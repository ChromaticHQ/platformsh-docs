---
title: "Changelog"
weight: 2
description: |
  Look here for all the most recent additions to Platform.sh.
---

{{< description >}}

## 2022

* **May 2022**
  * Support added for Dedicated plans using [MongoDb 5.0 Enterprise edition](../add-services/mongodb.md).
* **April 2022**
  * Dedicated Generation 3 adds support for [PostgreSQL](../add-services/postgresql.md).
  * Carbon intensity: You can now find information about the carbon intensity of each [region's energy grid](../development/regions.md).
* **March 2022**
  * The [`.platform/services.yaml` file](../add-services/_index.md) is no longer required.
    If you don't need services, you don't need to include the file in your repository.
  * Crons: added option to [cancel a cron activity](../create-apps/app-reference.md#crons)
  * Proxy routes: added option redirect requests to external locations with [proxy routes](../define-routes/proxy.md)
* **January 2022**
  * OpenSearch: Added [OpenSearch service](../add-services/opensearch.md)

## 2021

* **October 2021**
  * Regions: Added a [second region in Australia](../development/regions.md#australia), `au-2`.
* **September 2021**
  * Organizations: Switched to [organizations](../administration/organizations.md) for managing Platform.sh projects, users, and billing.
  * Vault: Added [Vault service](../add-services/vault.md).
  * .Net: We now support [.Net 5.0](../languages/dotnet.md).
* **May 2021**
  * Elasticsearch 6.8: We now support [Elasticsearch 6.8](../add-services/elasticsearch.md).
---
* **April 2021**
  * WAF: [a new page was added](../security/waf.md) describing the filtering rule sets and protections that come with the Platform.sh WAF.
  * [Build environment variables](../development/variables/set-variables.md#create-project-variables): environment variables can now accept the same `--visible-build` and `--visible-runtime` flags as project variables when created through the CLI. Build-visible variables are now a part of the build image ID, and therefore triggers a rebuild of the application when the value is updated. 
  * **Breaking change**: The logic by which the build image ID has changed in order to support build environment variables above. Previously, every attribute in `.platform.app.yaml` was included in the build image, used to create the unique build ID, and *accessible* via the `PLATFORM_APPLICATION` environment variable at build time. This is no longer the case, and only a subset of `.platform.app.yaml` attributes are now accessible from `PLATFORM_APPLICATION` at build time. See the [Platform.sh-provided variables](../development/variables/use-variables.md#use-platformsh-provided-variables) section for more information.
---
* **March 2021**
  * Observability: [a new page was added](../increase-observability/metrics/_index.md) describing observability and metrics available on Dedicated projects.
  * Node.js debugging: [a new page was added](../languages/nodejs/debug.md) that includes tips for debugging Node.js applications.
  * Parallel activities: [project activities](../integrations/activity/reference.md#maximum-activities-and-parallelism) have been split into separate queues, allowing for up to two activities across environments to occur simultaneously.
  * Python 3.9: We now support [Python 3.9](../languages/python.md).
  * Java 14: We now support [Java 14](../languages/java/_index.md).
  * PostgreSQL 13: [multiple databases](../add-services/postgresql.md#multiple-databases) are now supported for PostgreSQL 13.
  * Elasticsearch 7.9: We now support [Elasticsearch 7.9](../add-services/elasticsearch.md).
---
* **February 2021**
  * Elasticsearch 5.6: We now support [Elasticsearch 5.6](../add-services/elasticsearch.md) on Dedicated projects.
---
* **January 2021**
  * Default branch: [guide added](../environments/default-environment.md) that provides step for changing a project's default branch from `master` to `main`
---

## 2020

* **December 2020**
  * `us-4` region: We have [added](../development/regions.md) another US region, `us-4`.
---
* **September 2020**
  * Go 1.15: We now support [Go 1.15](../languages/go.md).
---
* **June 2020**
  * Node.js 14: We now support [Node.js 14](../languages/nodejs/_index.md).
---
* **April 2020**
  * We now offer [Xdebug on PHP](../languages/php/xdebug.md) containers.
  * Custom [activity scripts](../integrations/activity/_index.md) are now available, in alpha.
---
* **March 2020**
  * Go 1.14: We now support [Go 1.14](../languages/go.md).
  * Ruby 2.7: We now support [Ruby 2.7](../languages/ruby.md).
  * .NET Core: We now support [.NET Core 3.1](../languages/dotnet.md).
  * Memcached 1.6: We now support [Memcached 1.6](../add-services/memcached.md).
  * Solr 8.4: We now support [Solr 8.4](../add-services/solr.md).
---
* **February 2020**
  * Memcached 1.5: We now support [Memcached 1.5](../add-services/memcached.md).
  * Character set and collation are now configurable on [MySQL/MariaDB](../add-services/mysql/_index.md).
---
* **January 2020**
  * RabbitMQ: We now support [RabbitMQ virtual host configuration](../add-services/rabbitmq.md#virtual-hosts)
---

## 2019

* **December 2019**
  * Python 3.8: We now support [Python 3.8](../languages/python.md).
  * Node.js 12: We now support [Node.js 12](../languages/nodejs/_index.md).
  * RabbitMQ 3.8: We now support [RabbitMQ 3.8](../add-services/rabbitmq.md).
---
* **October 2019**
  * PHP 7.4: We now support [PHP 7.4](../languages/php/_index.md).
---

* **October 2019**
  * Projects can now have larger application containers in development environments.
---

* **September 2019**
  * "Dark mode" now available in the Console.
  * Go 1.13: We now support [Go 1.13](../languages/go.md).
---

* **July 2019**
  * Elasticsearch 7.2: We now support [Elasticsearch 7.2](../add-services/elasticsearch.md).
  * [Elasticsearch](../add-services/elasticsearch.md) 5.2 and 5.4 support is now deprecated
  * Kafka 2.2: We now support [Kafka 2.2](../add-services/kafka.md).
  * Java 13: We now support [Java 13](../languages/java/_index.md).
---

* **June 2019**
  * Java: We support and documented the use of [Java](../languages/java/_index.md) runtimes 8, 11, and 12, that includes examples that use the [Java Config Reader](https://github.com/platformsh/config-reader-java/).
  * Headless Chrome: Users can now define a [Headless Chrome](../add-services/headless-chrome.md) service to access a service container with a headless browser, which can be used for automated UI testing.
---

* **May 2019**
  * InfluxDB: We now support [InfluxDB](../add-services/influxdb.md) 1.7.
  * Solr 7 & 8: We now support [Solr](../add-services/solr.md) 7.7 and 8.0.
---

* **April 2019**
  * Network storage service: Users can now define a [Network storage](../add-services/network-storage.md) service for sharing files between containers.
  * Kafka message queue service: Users can now define a [Kafka](../add-services/kafka.md) service for storing, reading and analysing streaming data.
  * Management Console: Images and wording updated throughout entire documentation alongside [Management Console](../administration/web/_index.md) release.
---

* **March 2019**
  * Ruby 2.6: A new version of [Ruby](../languages/ruby.md) is now available.
  * Go 1.12: We now support [Go 1.12](../languages/go.md).
  * Elasticsearch 6.5: We now support [Elasticsearch 6.5](../add-services/elasticsearch.md).
---

* **January 2019**
  * RabbitMQ 3.7: We now support [RabbitMQ 3.7](../add-services/rabbitmq.md).
  * Solr 7: We now support [Solr 7.6](../add-services/solr.md).
  * Varnish: We now offer [Varnish](../add-services/varnish.md) 5.2 and 6.0.
---

## 2018

* **December 2018**
  * Elasticsearch 5.4: We now offer [Elasticsearch 5.4](../add-services/elasticsearch.md).
  * Improved Bash support: Bash history on application containers now persists between logins.
  * PHP 7.3: We now support [PHP 7.3](../languages/php/_index.md).
  * PostgreSQL 10.0 and 11.0: We now support [PostgreSQL 10.0 and 11.0](../add-services/postgresql.md) with an automated upgrade path.
  * Ruby 2.5 out of beta: We now fully support [Ruby 2.5](../languages/ruby.md).
---

* **October 2018**
  * Redis updates: [Redis 4.0 and 5.0](../add-services/redis.md) are now supported.
  * Go language support: [Go](../languages/go.md) is now a fully supported language platform.
---

* **September 2018**
  * Python 3.7 support: We now support [Python 3.7](../languages/python.md).
---

* **August 2018**
  * New public Canadian region: Our new Canadian region is now open for business.
---

* **July 2018**
  * Security and Compliance: We have created a new "Security and Compliance" section to help customers address common questions relating to GDPR, Data Collection, Data Retention, Encryption, and similar topics.
---

* **June 2018**
  * Node.js 10: We now offer [Node.js version 10](../languages/nodejs/_index.md). All releases in the 10.x series will be included in that container.
  * MongoDB 3.6: We now offer [MongoDB 3.2, 3.4, and 3.6](../add-services/mongodb.md). Note that upgrading from MongoDB 3.0 requires upgrading through all intermediary versions.
---

* **March 2018**
  * Web Application Firewall (WAF): Platform.sh is securing your applications and you don't need to change anything. Read more on our [blog post](https://platform.sh/blog/announcing-the-platformsh-waf).
---

* **February 2018**
  * `post_deploy` hook added: Projects can now run commands on deploy but [without blocking new requests](../create-apps/hooks/hooks-comparison.md#post-deploy-hook).

## 2017

* **December 2017**
  * New project subdomains: The routes generated for subdomains and literal domains in development environments will now use `.` instead of translating them to `---`, for projects created after this date.
  * `!include` tag support in YAML files: All YAML configuration files now support a generic [`!include`](../overview/yaml.md) tag that can be used to embed one file within another.
  * Extended mount definitions: A new syntax has been added for defining [mount points](../create-apps/app-reference.md#mounts) that is more self-descriptive and makes future extension easier.
  * Blocking older TLS versions: It is now possible to disable support for [HTTPS requests](../define-routes/https.md) using older versions of TLS. TLS 1.0 is known to be insecure in some circumstances and some compliance standards require a higher minimum supported version.
  * `{all}` placeholder for routes: A new placeholder is available in [`routes.yaml`](../define-routes/_index.md) files that matches all configured domains.
  * GitLab source code integration: Synchronize Git repository host on [GitLab](../integrations/source/gitlab.md) to Platform.sh.
---

* **November 2017**
  * PHP 7.2 supported: With the release of PHP 7.2.0, Platform.sh now offers [PHP 7.2](../languages/php/_index.md) containers on Platform Professional.
---

* **September 2017**
  * Health notifications: Low-disk warnings will now trigger a [notification](../integrations/notifications.md) via email, Slack, or PagerDuty.
---

* **August 2017**
  * Worker instances: Applications now support [worker instances](../create-apps/app-reference.md#workers).
---

* **July 2017**
  * Node.js 8.2: [Node.js 8.2](../languages/nodejs/_index.md) is now available.
---

* **June 2017**
  * Memcache 1.4: [Memcache 1.4](../add-services/memcached.md) is now available as a caching backend.
  * Custom static headers in `.platform.app.yaml`: Added support for setting custom headers for static files in `.platform.app.yaml`. [See the example](../create-apps/web/custom-headers.md) for more information.
---

* **May 2017**
  * Code-driven variables in `.platform.app.yaml`: Added support for setting [environment variables via `.platform.app.yaml`](../create-apps/app-reference.md#variables).
  * Python 3.6, Ruby 2.4, Node.js 6.10: Added support for updated versions of several languages.
---

* **April 2017**
  * Support for automatic SSL certificates: All production environments are now issued an SSL certificate automatically through Let's Encrypt.
    See the [routing documentation](../define-routes/https.md) for more information.
  * MariaDB 10.1: MariaDB 10.1 is now available (accessible as `mysql:10.1`).
    Additionally, both MariaDB 10.0 and 10.1 now use the Barracuda file format with `innodb_large_prefix` enabled,
    which allows for much longer indexes and resolves issues with some UTF-8 MB use cases.
---

* **March 2017**
  * Elasticsearch 2.4 and 5.2 with support for plugins: Elasticsearch 2.4 and 5.2 are now available.
    Both have a number of optional plugins available.
    See the [Elasticsearch documentation](../add-services/elasticsearch.md) for more information.
  * InfluxDB 1.2: A new service type is available for InfluxDB 1.2, a time-series database.
    See the [InfluxDB documentation](../add-services/influxdb.md) for more information.
---

* **February 2017**
  * HHVM 3.15 and 3.18: Two new HHVM versions are now available.
---

* **January 2017**
  * Support for Multiple MySQL databases and restricted users: MySQL now supports multiple databases, and restricted users per MySQL service.
    See the [MySQL documentation](../add-services/mysql/_index.md) for details or read our [blog post](https://platform.sh/2017/02/multi-mysql).
  * Support for Persistent Redis services:
    Added a `redis-persistent` service that is appropriate for persistent key-value data.
    The `redis` service is still available for caching.
    See the [Redis documentation](../add-services/redis.md) for details.
  * Support Apache Solr 6.3 with multiple cores:
    Added an Apache 6.3 service, which can be configured with multiple cores.
    See the [Solr documentation](../add-services/solr.md) for details.
  * Support for HTTP/2:
    Any site configured with HTTPS will now automatically support HTTP/2.
    Read more on our [blog post](https://platform.sh/2017/1/http2).
---

## 2016

* **December 2016**
  * Support async PHP:
    Deploy applications like ReactPHP and Amp which allow PHP to run as a single-process asynchronous process.
    Read a [blog post about PHP 7.1](https://platform.sh/2016/12/php-71).
  * Pthreads: Multithreaded PHP:
    PHP 7.1 containers are running PHP 7.1 ZTS, and include the Pthreads extension.
    Read a [blog post about multithreaded PHP](https://platform.sh/2016/12/php-71/#pthreads-multithreaded-php).
  * PHP 7.1: See [documentation for PHP](../languages/php/_index.md).
  * Support `.environment` files:
    This file is sourced as a bash script when a container boots up and on all SSH logins.
    See [more on `.environment` files](../development/variables/set-variables.md#set-variables-via-script).
  * Support `web.commands.start` for PHP:
    That option wasn't available for PHP as PHP only has one applicable application runner, PHP-FPM.
    It's now available for PHP.
    Read more at the [blog post](https://platform.sh/2016/12/app-updates-php/).

---

* **November 2016**
  * Customizable build flavor:
    Added a `none` build flavor which will not run any specific command during the build process. 
    Use it if your application requires a custom build process which can be defined in your build hook.
    Read more in our [blog post](https://platform.sh/2016/11/fully-customizable-build-flavors/).
---

* **October 2016**
  * PostgreSQL 9.6: Service is [documented here](../add-services/postgresql.md).
  * PostgreSQL extensions: Read more in our [blog post](https://platform.sh/blog/the-new-and-newer-postgresql/).
  * Node.js 6.8: Language is [documented here](../languages/nodejs/_index.md).
---

* **September 2016**
  * Python 2.7 & 3.5: Language is [documented here](../languages/python.md).
  * Ruby 2.3: Language is [documented here](../languages/ruby.md).
---

* **August 2016**
  * Support GitFlow: Read more in our [blog post](https://platform.sh/2016/08/gitflow-is-now-supported/).
---

* **July 2016**
  * Block Httpoxy security vulnerability: We bypass the [Httpoxy](https://httpoxy.org/) security vulnerability by blocking the Proxy header from incoming HTTP headers. Read more in our [blog post](https://platform.sh/2016/07/httpoxy/).
  * Remove default configuration files:
    We are removing the default configuration files that were previously used if your project didn't include one.
    You now need to include configuration files to deploy your applications on Platform.sh.
    Read more in our [blog post](https://platform.sh/2016/07/no-more-default-configuration-files/).
---

* **June 2016**
  * June update is summarized in our [blog post](https://platform.sh/2016/06/new-features-june/).
  * New PLATFORM_PROJECT_ENTROPY variable:
    New variable which has a random value, stable throughout the project's life.
    It can be used for Drupal hash salt for example (in our [Drupal 8 example](https://github.com/platformsh-templates/drupal8)).
    See a [reference for the variable](../development/variables/use-variables.md#use-platformsh-provided-variables)
  * Extend PLATFORM_RELATIONSHIPS variable: Expose the hostname and IP address of each service in the `PLATFORM_RELATIONSHIPS` environment variable.
  * Services updates: Update MongoDB client to 3.2.7, Node.js to 4.4.5, Blackfire plugin to 1.10.6, Nginx to 1.11.1.
---

* **May 2016**
  * May update is summarized in our [blog post](https://platform.sh/2016/05/new-features-may/).
  * Pre-warms Composer cache before executing Composer: The `composer` build flavor now pre-warms the Composer cache before executing Composer.
  * New image processing packages (advancecomp, jpegoptim, libjpeg-turbo-progs, optipng, pngcrush): Various image processing packages were added: advancecomp, jpegoptim, libjpeg-turbo-progs, optipng, pngcrush.
  * Security updates: Including imagetragick, glibc issue, various Java, OpenSSL and OpenSSH issues, along with some Git CLI vulnerabilities.
---

* **April 2016**
  * White label capabilities (Magento Enterprise Cloud Edition):
    Support for Platform.sh white label offering.
    First launch at Magento Imagine 2016 in Las Vegas of Magento Enterprise Cloud Edition.
---

* **March 2016**
  * CloudWatt deployment: Platform.sh is now available on Cloudwatt Orange Business Services hosted infrastructure.
    Read more in our [blog post](https://platform.sh/2016/03/platform-available-on-cloudwatt-by-orange/).
---

* **January 2016**
  * Redis 3.0: Service is [documented here](../add-services/redis.md).
---

## 2015

* **December 2015**
  * Node.js 0.12, 4.4 & 6.2: Read more in our [blog post](https://platform.sh/2015/12/release-nodejs)
---

* **November 2015**
  * Java Ant & Maven build scripts:
    Java Ant and Maven build scripts is supported for PHP 5.6 and up.
    Your application can pull and use most of Java dependency. Read more in our [blog post](https://platform.sh/2015/11/support-maven-and-ant)
---

* **October 2015**
  * MariaDB/MySQL 10.0: Service is [documented here](../add-services/mysql/_index.md).
  * MongoDB 3.0: Service is [documented here](../add-services/mongodb.md).
---

* **September 2015**
  * PHP 5.4, 5.5 & 5.6: Read more in our [blog post](https://platform.sh/2015/09/release-php)
  * RabbitMQ 3.5: Service is [documented here](../add-services/rabbitmq.md). Read more in our [blog post](https://platform.sh/2015/09/release-rabbitmq)
  * HHVM 3.9 & 3.12: Read more in our [blog post](https://platform.sh/2015/09/release-hhvm)
---

* **July 2015**
  * Documentation 3.0 release: Read more in our [blog post](https://platform.sh/2015/07/release-docs-3-0).
---

* **June 2015**
  * Bitbucket integration: This add-on allows you to deploy any branch or pull request on a fully isolated Platform.sh environment with a dedicated URL. Read more in Bitbucket's [blog post](https://bitbucket.org/blog/bitbucket-platform-sh-remove-the-middle-man-between-your-code-and-your-deployment).
  * PostgreSQL 9.3: Service is [documented here](../add-services/postgresql.md).
---

* **May 2015**
  * UI 2.0 release: Read more in our [blog post](https://platform.sh/2015/05/release-ui-2-0).
---

* **February 2015**
  * Blackfire integration: PHP applications come pre-installed with [Blackfire](https://blackfire.io/) developed by [SensioLabs](https://sensiolabs.com/). Read more in our [blog post](https://platform.sh/blackfire-integration).
---

* **January 2015**
  * Redis 2.8: Service is [documented here](../add-services/redis.md).
---

## 2014

* **November 2014**
  * Read more about this release in our [blog post](https://platform.sh/blog/2014/caching-custom-php-build-dependencies).
  * HTTP caching per route: Support for HTTP caching at the web server level, finely configurable on a per-route basis.
  * Custom PHP configurations: Support for tweaking the PHP configuration, by enabling / disabling extensions and shipping your own php.ini.
  * Build dependencies: Support for specifying build dependencies, i.e. PHP, Python, Ruby or Node.js tools (like SASS, Grunt, UglifyJS, and more) that you want to use to build your PHP application.
  * Elasticsearch 0.90, 1.4 & 1.7: Service is [documented here](../add-services/elasticsearch.md).
---

* **October 2014**
  * Automated protective block:
    Platform.sh provides a unique approach to protect your applications from known security issues.
    An automated protective blocking system which works a bit like an antivirus:
    it compares the code you deploy on Platform.sh with a database of signatures of known security issues in open source projects.
    This feature is [documented here](../security/protective-block.md).
    Read more in our [blog post](https://platform.sh/2014/10/21/protecting-your-apps).
  * Solr 4.10: Service is [documented here](../add-services/solr.md).
---

* **July 2014**
  * MariaDB/MySQL 5.5: Service is [documented here](../add-services/mysql/_index.md).
  * Solr 3.6: Service is [documented here](../add-services/solr.md).
---
