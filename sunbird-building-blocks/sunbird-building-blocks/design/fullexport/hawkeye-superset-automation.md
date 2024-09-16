# Hawkeye-Superset-Automation

### &#x20;Objective

Hawkeye superset is used to generate Analytics job config and report service config. From the initial implementation Hawkeye code was built on top of the exisiting forked repo from Apache superset.

From this automation implementation, superset core code will be taken upstream repo and Sunbird Hawkeye related code will be taken from a different repo and added together to build Hawkeye superset.

### Implementation Workflow

![](<../../../../Design/FullExport/images/storage/Hawkeye Automation.jpeg>)

### Hawkeye related files and usages of it

\| | Filename | File Path | Usage | File History | | Backend | report\_api.py | superset/report\_api.py | -> api call request to portal and analytics job apis -> Job config and portal config generation | New | | /superset | hawkeye\_chart.py | incubator-superset/superset/models/hawkeye\_chart.py | -> chart config model | New | | | hawkeye\_report.py | superset/models/hawkeye\_report.py | -> report config model | New | | | 9f2594aee0c4\_report\_migrations.py | superset/migrations/versions/9f2594aee0c4\_report\_migrations.py | hawkeye chart and report table migration | New | | | 11954187b979\_add\_interval\_slider\_hawkeye\_report.py | incubator-superset/superset/migrations/versions/11954187b979\_add\_interval\_slider\_hawkeye\_report.py | Interval slider implementation migration | New | | | bf1ec80c8c9a\_add\_static\_interval\_to\_hawkeye\_chart.py | superset/migrations/versions/bf1ec80c8c9a\_add\_static\_interval\_to\_hawkeye\_chart.py | static interval migration for hawkeye\_charts | New | | | 01defaf2ad37\_adding\_percentage\_topn\_config\_hawkeye.py | superset/migrations/versions/01defaf2ad37\_adding\_percentage\_topn\_config\_hawkeye.py | showing percentatage and top records migration to hawkeye\_charts | New | | | c5ecb4ef2220\_adding\_comments\_hawkeye\_charts.py | superset/migrations/versions/c5ecb4ef2220\_adding\_comments\_hawkeye\_charts.py | Comments to publish and reject the report | New | | | 4dde7c8b8f1b\_add\_dimension\_type\_hawkeye\_chart.py | superset/migrations/versions/4dde7c8b8f1b\_add\_dimension\_type\_hawkeye\_chart.py | parameterization implementation migration for hawkeye\_charts | New | | | b5cc2143b4bb\_add\_filters\_hawkeye\_charts.py | superset/migrations/versions/b5cc2143b4bb\_add\_filters\_hawkeye\_charts.py | filter config for hawkeye\_charts | New | | | 28b9fbb2e723\_add\_show\_table\_hawkeye\_charts.py | superset/migrations/versions/28b9fbb2e723\_add\_show\_table\_hawkeye\_charts.py | showing table implementation migration | New | | | b21497dbd5ab\_add\_show\_big\_number\_hawkeye\_charts.py | superset/migrations/versions/b21497dbd5ab\_add\_show\_big\_number\_hawkeye\_charts.py | showing big number implementation migration | New | | | slice.py | superset/models/slice.py | -> report url to redirect to hawkeye ui | Existing File | | | app.py | superset/app.py | -> Header and view builder changes - to add in flask-appbuilder | Existing File | | | core.py | incubator-superset/superset/views/core.py | -> Changes done for access verification | Existing File | | | views.py | incubator-superset/superset/views/chart/views.py | -> report chart list view injection implementation | Existing File | | | config.py | superset/config.py | Postgres host config changes | Existing File | | | manager.py | superset/security/manager.py | Report Role Creation changes added | Existing File | | | | | | | | Frontend | PublishChartButton.jsx | src/reportexplore/components/PublishChartButton.jsx | src/reportexplore/components/PublishChartButton.jsx | New | | /superset-frontend | ConfigModalBody.jsx | src/reportexplore/components/ConfigModalBody.jsx | Edit and view config for the report to Diksha | New | | | PublishStatusBody.jsx | src/reportexplore/components/PublishStatusBody.jsx | Publish button option's popup changes | New | | | ConfigInputControl.jsx | src/reportexplore/components/controls/ConfigInputControl.jsx | Input components generalized code | New | | | ReportChartList.tsx | src/views/reportChartList/ReportChartList.tsx | Adding Route | New | | | package.json | superset-frontend/package.json | Add @babel/compat-data | Existing File | | | ExploreViewContainer.jsx | src/reportexplore/components/ExploreViewContainer.jsx | Load report config data from backend to component | Existing File | | | ExploreActionButtons.jsx | src/reportexplore/components/ExploreActionButtons.jsx | Adding `Edit config` and `Publish` buttons | Existing File | | | ExploreChartHeader.jsx | src/reportexplore/components/ExploreChartHeader.jsx | Passing state data to child component | Existing File | | | ExploreChartPanel.jsx | src/reportexplore/components/ExploreChartPanel.jsx | Passing state data to child component | Existing File | | | QueryAndSaveBtns.jsx | src/reportexplore/components/QueryAndSaveBtns.jsx | Save button functional changes | Existing File | | | SaveModal.jsx | src/reportexplore/components/SaveModal.jsx | Save button functional changes | Existing File | | | exploreUtils.js | src/reportexplore/exploreUtils.js | API Endpoint configs | Existing File | | | main.less | src/reportexplore/main.less | css changes for modal elements | Existing File | | | webpack.config.js | webpack.config.js | adding reportexplore component entry point | Existing File | | | index.jsx | superset-frontend/src/reportexplore/index.jsx | Report explore page index component | Existing File | | | App.jsx | superset-frontend/src/welcome/App.jsx | Adding route for report list | Existing File |

### &#x20;Open Questions

| **Question**                                              | **Answer**                                                           |
| --------------------------------------------------------- | -------------------------------------------------------------------- |
| e.g., How might we make users more aware of this feature? | e.g., We'll announce the feature with a blog post and a presentation |

***

\[\[category.storage-team]] \[\[category.confluence]]