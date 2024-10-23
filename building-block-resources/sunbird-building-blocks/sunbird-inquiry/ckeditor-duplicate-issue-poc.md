---
icon: elementor
---

# CkEditor Duplicate Issue - POC

#### POC Solution <a href="#ckeditorduplicateissue-poc-pocsolution" id="ckeditorduplicateissue-poc-pocsolution"></a>

The solution proposed involves passing the `ClassicEditor` as an input to another library instead of importing it in every library.

#### Fixing the CKEditor Duplicate Issue in SunbirdEd-Portal <a href="#ckeditorduplicateissue-poc-fixingtheckeditorduplicateissueinsunbirded-portal" id="ckeditorduplicateissue-poc-fixingtheckeditorduplicateissueinsunbirded-portal"></a>

The areas where changes are required include:

* **common-form-elements-full**: Pass `ClassicEditor` as an input.
* **Questionset Editor**: Pass `ClassicEditor` as an input to the library/web component
* **Collection Editor**: Remove dead code related to the Questionset Editor from Collection Editor, including the `CKEditor` component and its dependencies. PRs have been raised for this past but are not yet in release branch:
  * [PR #593](https://github.com/Sunbird-Knowlg/sunbird-collection-editor/pull/593/files)
  * [PR #642](https://github.com/Sunbird-Knowlg/sunbird-collection-editor/pull/642)

#### Current Usage of CKEditor in All Libraries <a href="#ckeditorduplicateissue-poc-currentusageofckeditorinalllibraries" id="ckeditorduplicateissue-poc-currentusageofckeditorinalllibraries"></a>

```
import ClassicEditor from '@project-sunbird/ckeditor-build-classic';
ClassicEditor.create(this.editorRef.nativeElement, { ... ... });
```

We are importing and creating `ClassicEditor` in multiple places, causing the ckeditor-duplicate-error.

#### Proposed Solution <a href="#ckeditorduplicateissue-poc-proposedsolution" id="ckeditorduplicateissue-poc-proposedsolution"></a>

Instead of importing `ClassicEditor` in `sb-form`, `questionset-editor`, and `sunbirdEd-portal`, import it only in `sunbirdEd-portal` and pass `ClassicEditor` as input to `questionset-editor`. From `questionset-editor`, pass the same `ClassicEditor` as input to `sb-form`.

#### Implementation Notes <a href="#ckeditorduplicateissue-poc-implementationnotes" id="ckeditorduplicateissue-poc-implementationnotes"></a>

* **sunbirdEd-portal**: Refactor the import of `ClassicEditor` from individual components to a common service/helper service.
* **Questionset Editor**: Use `ClassicEditor` in the `CkeditorToolComponent` through a shared variable in `editor-service`.
* **SB-Form**: Accept `ClassicEditor` as an input and use it in the `dynamic-richtext` component.

#### Reference Code Changes <a href="#ckeditorduplicateissue-poc-referencecodechanges" id="ckeditorduplicateissue-poc-referencecodechanges"></a>

* [Editor Changes](https://github.com/Sunbird-inQuiry/editor/compare/release-8.0.0...rajnishdargan:8.0.0-wc?expand=1)

Note: `SB-Form` changes should be implemented before editor changes. In POC, the `ClassicEditor` dependency is commented out from `SB-Form` in `release-6.0.0` and installed in `Questionset Editor` with a local npm link.

* [SB-Form changes](https://github.com/Sunbird-Ed/SunbirdEd-forms/compare/release-6.0.0\_v14...rajnishdargan:release-6.0.0\_v14?expand=1) For POC

#### Additional Considerations <a href="#ckeditorduplicateissue-poc-additionalconsiderations" id="ckeditorduplicateissue-poc-additionalconsiderations"></a>

Installing the latest version of SB-Form in the editor is causing errors due to client-service dependency mismatches. Address issue [IQ-792](https://project-sunbird.atlassian.net/browse/IQ-792) before starting changes in `SB-Form` to pass `ClassicEditor` as input. Avoid merging vulnerability fixes PRs in `release-8.0.0` plan them for `next release` (becuase inQuiry release-8.0.0 is done in dev pushing these change in 8.0.0 will increase the testing effort)

#### Web Component Integration <a href="#ckeditorduplicateissue-poc-webcomponentintegration" id="ckeditorduplicateissue-poc-webcomponentintegration"></a>

Reference code change related to `questionset-editor` web component integration:

* [Test Editor WC](https://github.com/rajnishdargan/test-editor-wc)

#### Solving the Issue of Passing ClassicEditor as a Web Component <a href="#ckeditorduplicateissue-poc-solvingtheissueofpassingclassiceditorasawebcomponent" id="ckeditorduplicateissue-poc-solvingtheissueofpassingclassiceditorasawebcomponent"></a>

In inital POC, passing `ClassicEditor` to web components resulted in an empty object. This issue was resolved by passing `ClassicEditor` in the following form:

```
(questionsetEditorElement as any).ckEditorLib = this.ckEditorLib;
```

Reference: [App Component](https://github.com/rajnishdargan/test-editor-wc/blob/main/src/app/app.component.ts#L29)
