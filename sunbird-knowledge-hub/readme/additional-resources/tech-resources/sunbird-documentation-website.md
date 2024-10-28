---
icon: elementor
---

# Sunbird Documentation Website

### Sunbird Documentation Website <a href="#id-9cmramr2gs4u" id="id-9cmramr2gs4u"></a>

#### Project Scope <a href="#id-5gco6okquyds" id="id-5gco6okquyds"></a>

Sunbird Documentation website ( [http://docs.sunbird.org/](http://docs.sunbird.org/) ).

#### Project background <a href="#xl1pfq577jf4" id="xl1pfq577jf4"></a>

Sunbird being open-source project, it was required to host its documentation for each version, so that anyone can adopt it. Any contributor should be able to raise the pr with changes, and the reviewer should be able to review the changes before merging. [https://project-sunbird.atlassian.net/wiki/spaces/SBDES/pages/411893865/Docs+Versioning](https://project-sunbird.atlassian.net/wiki/spaces/SBDES/pages/411893865/Docs+Versioning)

#### URL’s <a href="#a7y73082yzo1" id="a7y73082yzo1"></a>

* Prod - [http://docs.sunbird.org/](http://docs.sunbird.org/)
* Staging - [http://qa.docs.sunbird.org/](http://qa.docs.sunbird.org/)
* PR Preview sites - [http://\<pr-id>.qa.docs.sunbird.org/](http://qa.docs.sunbird.org/) Eg - [http://234.qa.docs.sunbird.org/](http://234.qa.docs.sunbird.org/)
* Github - [https://github.com/project-sunbird/sunbird.org-docs/](https://github.com/project-sunbird/sunbird.org-docs/)
* CircleCI - [https://circleci.com/gh/project-sunbird/sunbird.org-docs](https://circleci.com/gh/project-sunbird/sunbird.org-docs)
* Docker Image - [https://hub.docker.com/r/lakhanmandloi/docker-ubuntu-ruby-python-npm](https://hub.docker.com/r/lakhanmandloi/docker-ubuntu-ruby-python-npm) and Github repo - [https://github.com/lakhanmandloi/docker-ubuntu-ruby-python-npm](https://github.com/lakhanmandloi/docker-ubuntu-ruby-python-npm)

#### Tools Used <a href="#qsasp8hl33xu" id="qsasp8hl33xu"></a>

* Jekyll ( [https://jekyllrb.com/](https://jekyllrb.com/) ) - Static site generator
* Docker - For Jekyll build environment and deployment processes
* CircleCI - A CI/CD tool
* Amazon S3 bucket - To hold staging and pr preview sites
* Proxy server - For qa and pr preview sites.

#### Prerequisites knowledge <a href="#kid5vzex72bv" id="kid5vzex72bv"></a>

* Jekyll
* Docker
* CircleCI
* AWS CLI
* JQ
* Github
* Curl
* Shell scripting

#### Pre-requisites <a href="#wgvws1k16do1" id="wgvws1k16do1"></a>

* Ruby ( [https://www.ruby-lang.org/en/](https://www.ruby-lang.org/en/) )
* Bundler ( [https://bundler.io/](https://bundler.io/) )
* sudo apt-get install zlib1g-dev
* sudo apt-get install build-essential
* Gem install nokogiri
* Clone [https://github.com/project-sunbird/sunbird.org-docs](https://github.com/project-sunbird/sunbird.org-docs/) repo, switch directory to the repo and run command bundle install . This will install all dependencies mentioned in Gemfile.

#### Repositories <a href="#sqfjrgw3yu44" id="sqfjrgw3yu44"></a>

* [https://github.com/project-sunbird/sunbird.org-docs](https://github.com/project-sunbird/sunbird.org-docs/) - This repo contains raw file in some branches as well as it hosts the production website on gh-pages branch. This repo has several branches which function as follows -
  * **gh-pages** - This branch holds the generated prod site. Version folder like 1.8, 1.9 contains the generated site from respective version branch while all other files and folder comes from toc branch. Note - all html files inside the version folder has its version folder as base url so that all relative urls resolves in its own version and there is no need to update urls in every version. Typical Folder structure -

| <ul><li>index.html</li><li>css/</li><li><p>js/</p><ul><li>widgets-data.js # Holds Version data</li><li>latest-version.txt # Holds latest version branch</li></ul></li><li>img/</li><li>latest/ # Symlink to the latest version folder</li><li>1.9/ # Holds site generated from branch 1.9</li><li>1.8/ # Holds site generated from branch 1.8</li></ul> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

*
  * **Version branches ( Eg - 2.2.0, 2.1.0, 1.9 )** - These branches contains version specific documentation in raw md / jekyll format.
  * **Master** - copy of the latest version
  * **toc branch** - This branch contains the main landing page of the site and css and js of entire site. Note - widgets.js creates widgets (Version changing dropdown and latest version available notice on old versions) on all version docs pages. Version docs pages contains the placeholder where these widget gets appended.

#### Proxy server and Amazon S3 bucket <a href="#id-6e36oa5nb6w3" id="id-6e36oa5nb6w3"></a>

Sunbird-docs-qa s3 bucket has 2 folders

* **docs-staging** - this folder hosts the staging site. [qa.docs.sunbird.org](http://qa.docs.sunbird.org/) points to this folder via proxy server.
* **docs-pr** - this folder has several sub-folder. Each pr raised creates a folder inside this docs-pr folder with name \<pr-id>. The proxy server points ( Wildcard entry ) \<pr-id>.qa.docs.sunbird.org folder to this \<pr-id> folder so that each pr has its own subdomain.

#### Build processes <a href="#ysz47td7xui5" id="ysz47td7xui5"></a>

Sunbird Docs uses CircleCI for build and deployments. Each branch has its own circleci config, but all configs are same except toc branch which requires different build processes. Version branches have workflow version-build-deploy while toc branch has toc-build-deploy

* [https://drive.google.com/open?id=12AUyVJYXuGj\_ATumy6vZ71pSYQX6FgL0](https://drive.google.com/open?id=12AUyVJYXuGj\_ATumy6vZ71pSYQX6FgL0)
* [https://circleci.com/gh/project-sunbird/workflows/sunbird.org-docs](https://circleci.com/gh/project-sunbird/workflows/sunbird.org-docs).

Both workflows have 4 jobs -

* **PR** - whenever any pr is raised this job is triggered. The site is generated and deployed to docs-pr/\<pr-id> folder of s3 bucket. With the help of \<pr-id> the pr info is fetched with apis using curl & jq. The info pulled from apis is - username, files modified. Based on files paths and pr id, the modified urls are identified and this info is posted as comment on that with the help of apis. This comment helps reviewer and contributor to easy verify the changes.
* **Staging** - Once the pr is merged i.e. commit happens in repo this build is triggered. This generates the site and deploys to docs-staging folder of s3 bucket. Once this job is successful, then passes control to hold job.
* **Hold** - This creates an approval popup on CircleCI, on approval of this, prod job is triggered.
* **Prod** - the generated site changes are fetched from the docs-staging folder and committed to the gh-pages branch.

#### Secrets stored in CircleCI <a href="#xg3eb4rn251z" id="xg3eb4rn251z"></a>

* Checkout SSH key - to fetch and commit changes to the repo - [https://circleci.com/gh/project-sunbird/sunbird.org-docs/edit#checkout](https://circleci.com/gh/project-sunbird/sunbird.org-docs/edit#checkout)
* S3 bucket - Access key Id and Secret access key - [https://circleci.com/gh/project-sunbird/sunbird.org-docs/edit#aws](https://circleci.com/gh/project-sunbird/sunbird.org-docs/edit#aws)
* Github - API token, user email address, username and ssh fingerprint. - [https://circleci.com/gh/project-sunbird/sunbird.org-docs/edit#env-vars](https://circleci.com/gh/project-sunbird/sunbird.org-docs/edit#env-vars)
