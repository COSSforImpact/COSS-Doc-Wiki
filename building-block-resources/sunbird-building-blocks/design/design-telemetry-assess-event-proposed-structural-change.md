---
icon: elementor
---

# \[Design] - Telemetry ASSESS Event proposed structural change

* Introduction
* Background
* Key Design Problems
* Solutions
  * Identify the question type
  * Bound the edata.resvalues keys
  * Capture options are shown and enhance resvalues
    * MCQ
    * FTB
    * MTF
    * Sequence
    * ReOrder

### **Introduction** <a href="#id-design-telemetryassesseventproposedstructuralchange-introduction" id="id-design-telemetryassesseventproposedstructuralchange-introduction"></a>

This wiki details the current problems/issues with the ASSESS telemetry event data and proposed changes/fixes to it. The telemetry event data is either not captured in entirely that is useful for analysis or complex to analyze.

### **Background** <a href="#id-design-telemetryassesseventproposedstructuralchange-background" id="id-design-telemetryassesseventproposedstructuralchange-background"></a>

Please refer the below wiki for the telemetry events generated as of now for various question types.

[**Question-set telemetry ASSESS event**](https://project-sunbird.atlassian.net/wiki/spaces/SBDES/pages/952336531/Question-set+telemetry+ASSESS+event)

As part of the analysis, we found that event structure is not common & it is very hard to analyze. Not enough data is captured to be able to do any meaningful analysis.

Following are some of the issues we have identified:

* Telemetry ASSESS event has > 6k key-value pairs under 'edata.resvalue' field. This is due to unbounded keys. For ex: - Every mcq question is generating a unique key for the {key:value} pair.
* Telemetry ASSESS event doesn’t have information about what is the type of question. Without this information any custom analysis to be done dependent on the type of question is not possible unless a search is performed for the question type in the content index with the given question id.
* Telemetry ASSESS event “edata” doesn’t have information about how the question was rendered/shown to the user. For ex: What are the options were shown to the user for MCQ question and in what order (options can be shuffled).
* There is no consistency of capturing “resvalues” across all question types.
* In FTB/MMCQ where there is a possibility of partial scoring and the params should capture the correct options.

### **Key Design Problems** <a href="#id-design-telemetryassesseventproposedstructuralchange-keydesignproblems" id="id-design-telemetryassesseventproposedstructuralchange-keydesignproblems"></a>

* Identify the type of question
* Bound the “edata.resvalues” keys to not more than 20 keys across all possible question types
* Capture the options shown & the order of the options rendered to the user in the edata.item.params field
* Capture additional required information in the “value” field of “edata.resvalues”.

### **Solutions** <a href="#id-design-telemetryassesseventproposedstructuralchange-solutions" id="id-design-telemetryassesseventproposedstructuralchange-solutions"></a>

#### **Identify the question type** <a href="#id-design-telemetryassesseventproposedstructuralchange-identifythequestiontype" id="id-design-telemetryassesseventproposedstructuralchange-identifythequestiontype"></a>

Telemetry spec is updated to send “type” of the question as part of the field - “edata.item.type”. Following are the currently possible question types:

1. **mcq** - Multiple choice questions
2. **ftb** - Fill in the blank
3. **mtf** - Match the following
4. **sequence** - Sequence the shown sentences to make a paragraph
5. **reorder** - Reorder the shown text options to frame a sentence

#### **Bound the edata.resvalues keys** <a href="#id-design-telemetryassesseventproposedstructuralchange-boundtheedata.resvalueskeys" id="id-design-telemetryassesseventproposedstructuralchange-boundtheedata.resvalueskeys"></a>

Unbounded keys are resulting in too many key-value pairs being generated which have become a challenge during data analysis. Hence the approach is to bound the keys generated either by index or via pre-defined keys for each question type.

Following is the approach for each question type:

1. **MCQ** - The currently supported max options are 8. Hence an index from 1 to 8 as key for both `edata.item.params` and `edata.resvalues` would bound the possible keys to 8. For ex: `edata.item.params` would have the data shown to user as `"params":[{"1":""},{"2":""},{"3":""},{"4":""}]` for 4 options and the `edata.resvalues` would have data as `"resvalues":[{"2":""}]` denoting the selected option.
2. **FTB** - The currently supported max options are not defined but assumed to be not more than 20 (considering the mobile display size). Hence an index from 1 to 20 as key for both `edata.item.params` and `edata.resvalues` would bound the possible keys approximately to 20. The index is the position where the blank option is shown. For ex: `edata.item.params` would have the expected blank values as `"params":[{"1":""},{"2":""},{"3":""},{"4":""}]` for 4 options and the `edata.resvalues` would have data as `"resvalues":[{"1":""},{"2":""},{"3":""},{"4":""}]` denoting the entered values in the blanks.
3. **MTF** - For match the following the options are fixed. It is always to capture either the data shown in lhs and rhs to user or the user arrangement of lhs and rhs. Hence there would be two keys here `lhs` and `rhs` and one more key to denote the right match which is `answer`.
4. **Sequence** - Similar to mtf, this is to arrange the sentences in a sequence to form a paragraph. The max possible options that can be configured are 8, hence an index from 1 to 8 as key for both `edata.item.params` and `edata.resvalues` would bound the possible keys to 8. In addition there would be one more key to capture the correct sequence as well so that the total bound keys would be 9. For ex: `edata.item.params` would have the data shown to the user as `"params":[{"1":""},{"2":""},{"3":""},{"4":""},{"answer":"'['3','2','1','4']'"}]` for 4 options and one key to capture the correct sequence and the `edata.resvalues` would have data as `"resvalues":[{"3":""},{"2":""},{"1":""},{"4":""}]` denoting the rearranged sequence.
5. **Reorder** - This is similar to sequence, wherein the sequence is to re-order the sentences into a paragraph, the re-order type of question is to re-order the various text options shown to form a sentence. The only difference is that the number of text options are not bounded, but assuming to be not more than 20 (anything more than 10 will have display issues). So the probable count the keys can be bound to can be approximately 20.

So the final bound keys will be approximately `23` -

```
MCQ = [1,2,...,8,answer]
FTB = [1,2,...,20,eval]
MTF = [lhs,rhs,answer]
Sequence = [1,2,3,4,5,6,7,8,answer]
Reorder = [1,2,3,...,20,answer]
```

#### **Capture options are shown and enhance resvalues** <a href="#id-design-telemetryassesseventproposedstructuralchange-captureoptionsareshownandenhanceresvalues" id="id-design-telemetryassesseventproposedstructuralchange-captureoptionsareshownandenhanceresvalues"></a>

The existing telemetry only captures the option shown which can be a text or an image asset id or an audio asset id. Wherever there are multiple values shown like an option containing both text and image, only partial information is captured. Therefore we are now enhancing it to show the complete metadata.

`text` : Options/Answers text.

`image`: Image asset ID.

`audio`: Audio asset ID.

Following are the detailed examples of the proposed data capture for all question types.

**MCQ**

![](<../../../.gitbook/assets/grey\_arrow\_down (5).png>)rendered options

```
{
  "params": [
    { "1": "{'text': 'Venus','image': 'do_126763636355262','audio': 'do_145897733222234455'}" },
    { "2": "{'text': 'Mars','image': 'do_123689743353533','audio': 'do_1236873635363635363'}" },
    { "answer": "{'correct': ['2']}" }
  ]
}
```

![](<../../../.gitbook/assets/grey\_arrow\_down (5).png>)selected options

```
{
  "resvalues": [
     { "2": "{'text': 'Mars','image': 'do_123689743353533','audio': 'do_1236873635363635363'}" }
  ]
}
```

**FTB**

![](<../../../.gitbook/assets/grey\_arrow\_down (5).png>)rendered options

```
{
  "params": [
   { "1": "{'text': 'Venus'}" },
   { "2": "{'text': 'Mars'}" },
   { "eval": "order" }
  ]
}
```

![](<../../../.gitbook/assets/grey\_arrow\_down (5).png>)selected options

```
{
  "resvalues": [
    "2": "{'text': 'Mars'}"
  ]
}
```

**MTF**

![](<../../../.gitbook/assets/grey\_arrow\_down (5).png>)rendered options

```
{
  "params": [
      { "lhs": "[{'1': '{'text': 'Venus','image': '','audio': ''}'}, {'2': '{'text': 'Jupiter','image': '','audio': ''}'},{'3': '{'text': 'Earth','image': '','audio': ''}'}]" },
      { "rhs": "[{'1': '{'text': 'Water Planet','image': '','audio': ''}'}, {'2': '{'text': 'Hottest Planet','image': '','audio': ''}'},{'3': '{'text': 'Biggest planet','image': '','audio': ''}'}]" },
      { "answer": "{'lhs': ['1','2','3','4'], 'rhs': ['3','2','4','1']" }
    ]
}
```

![](<../../../.gitbook/assets/grey\_arrow\_down (5).png>)selected options

```
{
  "resvalues": [
      { "lhs": "[{'1': '{'text': 'Venus','image': '','audio': ''}'}, {'2': '{'text': 'Jupiter','image': '','audio': ''}'},{'3': '{'text': 'Earth','image': '','audio': ''}'}]" },
      { "rhs": "[{'1': '{'text': 'water Planet','image': '','audio': ''}'}, {'2': '{'text': 'Hottest Planet','image': '','audio': ''}'},{'3': '{'text': 'Biggest planet','image': '','audio': ''}'}]" }
    ]
}
```

**Sequence**

![](<../../../.gitbook/assets/grey\_arrow\_down (5).png>)rendered options

```
{
  "params": [
      { "1": "{'text': 'is','image': '','audio': ''}" },
      { "2": "{'text': 'Rose','image': '','audio': ''}" },
      { "3": "{'text': 'Red','image': '','audio': ''}" },
      { "answer": "{'seq':['3','2','1']}"}
    ]
}
```

![](<../../../.gitbook/assets/grey\_arrow\_down (5).png>)selected options

```
{
  "resvalues": [
      { "3": "{'text': 'Red','image': '','audio': ''}" },
      { "1": "{'text': 'is','image': '','audio': ''}" },
      { "2": "{'text': 'Rose','image': '','audio': ''}" }
    ]
}
```

**ReOrder**

![](<../../../.gitbook/assets/grey\_arrow\_down (5).png>)rendered options

```
{
  "params": [
      { "1": "{'text': 'Red'}" },
      { "2": "{'text': 'Rose'}" },
      { "3": "{'text': 'is'}" },
      { "answer": "{'seq':['3','2','1']}"}
    ]
}
```

![](<../../../.gitbook/assets/grey\_arrow\_down (5).png>)selected options

```
{
  "resvalues": [
    { "2": "{'text': 'Rose'}" }
  ]
}
```
