# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).


## [2.2.0] - Unreleased
### Added
- Added `patch` method to client to allow for partial document updates
- Added `deleteById` method to client to prevent overhead of Document-based deletions when identifier and index are known
- Added the ability to pass request parameters to deletion methods
- Added a new `patch` method to `IndexBuilder.cfc` which provides a more intuitive API for partial updates to indices and settings
- Adds a new `processBulkOperation` method for performing [bulk operations with multiple actions](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-bulk.html)
- Additional error handling for non-JSON responses from Elasticsearch servers
### Fixed
- Typos in documentation in docblocks


## [2.1.2] - 2020-12-11

### Fixed
- Issue #76 - Fixes an incorrect error response typing

## [2.1.1] - 2020-12-07

### Added
- Additional documentation updates
- Improve error response by passing all response errors through a single parsing method
- Add handling for root cause exceptions on shard failure ( Issue #65 )

### Fixed
- Issue #72 - Fixes a bug where the node pool was not using the full length of the pool
- Issue #74 - Fixes a regression in `filterTerms` query DSL generation

## [2.1.0] - 2020-12-03

### Changed
- Modifies LogstashAppender schema to match default 7.x logstash template and adds additional schema keys and hooks for Stachebox

### Added
- Adds the `collapseToFields` method to the search builder to support documents grouped on a specific field.

## [2.0.5] - 2020-11-25

### Added
- Adds the ability to specify an operator to term queries via `filterTerm` and `filterTerms` and pass multiple values to filter

## [2.0.4] - 2020-11-04

### Changed
- Lowers the default number of Logstash shards on index to 2, to prevent inheritance of application shard settings
- Lowers the default number of Logstash replicas to 0, to prevent maximum shard errors
- Changes the default Logstahs index rotation frequency to weekly

## [2.0.3] - 2020-10-13

### Fixed
- Fixes an error in the Logstash appender which could be thrown by a non-string value in the exception object `type` key

## [2.0.2] - 2020-09-15

### Added
- Adds additional data and exception information in Logstash appender messages

## [2.0.1] - 2020-09-10

### Added
- Adds Logstash appender and converts Elasticsearch appender to use Logstash schema for index data
- Adds a `wildcard` method to Search builder for wildcard searches on keyword-mapped fields

## [2.0.0] - 2020-09-01

### Changed
- Converts default native client to HyperClient ( native CFML implementation )
- Removes the `deleteMapping` method in the main client, as it is no longer supported in ES versions 6.5 and up.
- Removes support for Adobe Coldfusion 11
- Removes support for Lucee 4.x
- Moves previous native JEST Client to [`cbelasticsearch-jest` module](https://forgebox.io/view/cbelasticsearch-jest).
- Ends official support for 6.x versions of Elasticsearch

### Added
- Adds `cbElasticsearchPreSave` and `cbElasticsearchPostSave` interceptions when saving individual or bulk documents
- Adds the ability to create, update, read, and delete [Elasticsearch pipelines](https://www.elastic.co/guide/en/elasticsearch/reference/master/ingest-apis.html)
- Adds the ability to configure a pipeline for document processing ( e.g. `myDocument.setPipeline( 'my-pipeline' )` )
- Adds the ability to add save [query parameters](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-index_.html#docs-index-api-query-params) when saving individual documents ( e.g. `myDocument.addParam( 'refresh', true )` )
- Adds the ability to pass a struct of [params to bulk save operations](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-bulk.html#docs-bulk-api-query-params) (e.g. `client.saveAll( documents, false, { "refresh" : true } )` )

## [1.4.1] - 2020-02-27

### Fixed
- Fixes an issue where a null value would throw an error when creating a native Java HashMap

## [1.4.0] - 2020-02-22

### Added
- Adds new search builder methods `suggestTerm`, `suggestPhrase`, and `suggestCompletion` for auto-completion and auto-suggestion queries
- Adds a throw on error argument, with a default of true, to client reindex() method when waiting for completion

### Fixed
- Fixes an issue where default shard/replica settings were being overwritten when passing a complete config

## [1.3.2] - 2020-02-12

### Changed
- Modifies search builder methods of `filterTerm` and `filterTerms` to return the builder instance ( Issue #43 )
- Modifies Document `setValue` method to return instance, for method chaining ( Issue #40 )

### Added
- Adds a Util component for common inbound and outbound conversions and casting

### Fixed
- Fixes an error when individual documents in a bulk save contained errors ( Issue #44 )

## [1.3.1] - 2019-12-13

### Added
- Adds responses to task model
- Adds the ability to provide a transformation script to the client `reindex` method

## [1.3.0] - 2019-11-28

### Added
- Adds the ability to pass URL parameters to SearchBuilder-aware client methods. Adds a `param( name, value )` supporting method to the SearchBuilder
- Adds a new Task object which can be refreshed and used in a loop as long-running tasks complete in the background ( e.g. `while( !task.isComplete() )` )
- ( Breaking ) Changes the return type of the `deleteByQuery` and `updateByQuery` to return the full API response which may be inspected or used to follow-up on tasks
- implements a `getAllTasks()` method in the client, which will return an array of Task objects
- implements a `getTask` method in the client to retreive tasks by identifier ( e.g. - `[node]:[id]` ).
- implements a `getIndices` method in the client to retreive a map of indices with stats
- implements a `getAliases` method in the client to retreive a map of aliases

### Fixed
- Resolves Issue #12 - slf4j missing on non-Runwar installations
- Resolves Issue #17 - implements workarounds and adds documentation on how to configure and use a connection to a secondary elasticsearch cluster

## [1.2.2] - 2019-10-23

### Added
- Adds fallback attempt when connection pool is unexpectedly closed upstream

## [1.2.1] - 2019-09-27

### Added
- Adds a soft fail to the version target check when a connection to the ES start page cannot be established

## [1.2.0] - 2019-09-26

### Added
- Implements compatibility for Elasticsearch v7
- Adds environment variable detection for default configuration
- Implements a new AliasBuilder object, which can be used to alias indexes
- Implements a new `reindex()` method in the client which allows the ability to reindex
- Implements new `mustExist` and `mustNotExist` methods to the SearchBuilder

## [1.1.6] - 2019-06-21

### Changed
- Reverts to previous versions of HTTP client due to instability and connection expiration issues

### Added
- Adds connection cleanup prior to execution

## [1.1.5] - 2019-06-20

### Changed
- Updates Apache HTTP Client to v4.5.9

### Added
- Adds count() methods to the SearchBuilder and Client

## [1.1.4] - 2019-06-03

### Changed
- Implements url encoding for identifiers, to allow for spaces and special characters in identifiers

## [1.1.3] - 2019-05-11

### Added
- Implements update by query API and interface

## [1.1.2] - 2019-04-24

### Added
- Adds compatibility when Secure JSON prefix setting is enabled

## [1.1.1] - 2020-04-17

### Changed
- Updates Java Dependencies, including JEST client, to latest versions

### Added
- Implements search term highlighting capabilities

## [1.1.0] - 2020-02-27

### Changed
- Updates to `term` and `filterTerms` SearchBuilder methods to allow for more precise filtering

### Added
- Adds `filterTerm` method which allows restriction of the search context
- Adds `type` and `minimum_should_match` parameters to `multiMatch` method in SearchBuilder

## [1.0.0] - 2018-11-29

### Changed
- Updates to SearchBuilder to alow for more complex queries with fewer syntax errors
- Refactor filterTerms to allow other `should` or `filter` clauses

### Added
- Adds support for Elasticsearch v6.0+
- Adds a new MappingBuilder
- Add ability to specify `_source` excludes and includes in a query
- ACF Compatibility Updates

## [0.3.0] - 2017-11-16

### Added
- Adds `readTimeout` and `connectionTimeout` settings
- Adds `defaultCredentials` setting
- Adds default preflight of query to fix common assembly syntax issues

## [0.2.1] - 2017-10-01

### Added
- Adds `filterTerms()` method to allow an array of term restrictions to the result set

## [0.2.0] - 2017-09-23

### Added
- Adds support for terms filters in match()

### Fixed
- Fixes pagination and offset handling

## [0.1.0] - 2017-05-17

### Added
- Initial Release
