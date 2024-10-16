---
icon: elementor
---

# \[PRD] Multi-Lingual Support

## Objective <a href="#id-prd-multi-lingualsupport-objective" id="id-prd-multi-lingualsupport-objective"></a>

Create questions in multiple languages using the Editor and allow the Player to choose the preferred language from the options available, while playing a question/question set

## Fields that needs multilingual support <a href="#id-prd-multi-lingualsupport-fieldsthatneedsmultilingualsupport" id="id-prd-multi-lingualsupport-fieldsthatneedsmultilingualsupport"></a>

* body
* answer
* instructions
* feedback
* hints

## User Flow <a href="#id-prd-multi-lingualsupport-userflow" id="id-prd-multi-lingualsupport-userflow"></a>

### Scenario 1 : Create and consume questions & question set in any language <a href="#id-prd-multi-lingualsupport-scenario1-createandconsumequestions-and-questionsetinanylanguage" id="id-prd-multi-lingualsupport-scenario1-createandconsumequestions-and-questionsetinanylanguage"></a>

1. Editor
   1. User should be able to choose the required language(s) from a dropdown and create a question in that language
   2. A default list of languages will be available in the drop down. Additional languages to be displayed in the dropdown list can be configured.
      1. The language will be pre-selected as `English` by default.
      2. The user will be able to choose any language from the dropdown menu. The user should be able to type a language that is not in the drop down (free text input)
      3. User will be able to select maximum **five** languages
   3. Upon selecting a language, the corresponding language code will be stored.
   4. The language selection can be done is any of following pattern :
      1. `Option 1` _:_
         1. There will be a drop-down across each of the fields, for which multiple languages are supported.
         2. The language selected for the first field, will be retained as the default for the rest of the fields, unless selected otherwise.&#x20;
            1. Eg. While creating a question set, if the creator first chooses the language for the ‘instructions’ field as \`Hindi\`, the rest of the fields - ‘body’, ‘options’ etc, should automatically have ‘Hindi’ as default language.
      2. `Option 2` _:_
         1. There will be only one drop down where the language is selected, and will be applied for all fields within a question/question set.
      3. `Option 3`_:_
         1. Dropdown for language selection will be present at 3 places :
            1. At Question Set Root node, where it will cover the following
               1. Instructions (at the root node level)
            2. At each Section, where it will cover the following fields :
               1. Instruction (at the each section level)
            3. At each Question, where it will cover the following fields:
               1. Question body
               2. Options
               3. Solution
               4. Feedback
               5. Hint
   5. The user selects all the languages in which he/she wants to create the question/question set and the form will display text box based on the selection
   6. Corresponding text boxes for entering the text are displayed for all the selected languages
      1. A button/checkbox can be displayed which can show the translated text on-demand.
         1. Upon selecting the option, the input text are will show the translation of the original text (primary language) to the selected language.
   7. Creator is able to type or copy paste in any language (question body/instruction/options..)
      1. Incase the user selects a non-english language, the Google Input Tool prompt pops-up in the selected language.
   8. Validate if the entered language is same as the selected language.
      1.  If the entered language is different from the selected language, an error message will be displayed. This is not going to be a validation, it will just be an alert.\
          \
          **Proposed Reference Design for the Editor** (as per `Option 2`) **:**





1. Player
   1. A dropdown will be present at the beginning of the Question or Question set, that is selected for playing.
   2. The user will be able to choose any language based on the available languages in the dropdown.
      1. The language in the dropdown will be populated based on the languages in which the question / question set is available.
   3. The drop down can have multi-select options ie the user will be able to select multiple languages
      1. Player will be able to select maximum of **two** languages.
   4. The question / question set will be rendered in the selected language/languages
      1. The question level language selection will override the question set level language selection ie, the user will be able to view the question is any language that is available in the dropdown
   5. At each question level
      1. A dropdown option will be present at the beginning.
      2. The dropdown will display only the languages in which the question body is present.
      3. Upon selecting a language from the dropdown, the question will be displayed in the selected language.
         1. By default the language will be `English`
         2. Incase of MCQ, if the options are not present in the selected language, display the options from the default language.

**Proposed Reference Design for the Player:**



