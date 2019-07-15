# Dynamic Search | Index Provider: PHP Lucene

[![Software License](https://img.shields.io/badge/license-GPLv3-brightgreen.svg?style=flat-square)](LICENSE.md)
[![Latest Release](https://img.shields.io/packagist/v/dachcom-digital/dynamic-search-index-provider-lucene.svg?style=flat-square)](https://packagist.org/packages/dynamic-search-index-provider-lucene)
[![Travis](https://img.shields.io/travis/com/dachcom-digital/pimcore-dynamic-search-index-provider-lucene/master.svg?style=flat-square)](https://travis-ci.com/dachcom-digital/pimcore-dynamic-search-index-provider-lucene)
[![PhpStan](https://img.shields.io/badge/PHPStan-level%202-brightgreen.svg?style=flat-square)](#)

A Index Storage Extension for [Pimcore Dynamic Search](https://github.com/dachcom-digital/pimcore-dynamic-search). Store data with the PHP Lucene index service.

## Requirements
- Pimcore >= 5.8.0
- Pimcore Dynamic Search

***

## Basic Setup

```yaml

dynamic_search:
    context:
        default:
            index_provider:
                service: 'lucene'
                options:
                    database_name: 'my_lucene_storage'
```

***

## Provider Options

| Name                                 | Default Value          | Description |
|:-------------------------------------|:-----------------------|:------------|
|`database_name`                       | null                   |             |
|`force_adding_document`               | true                   |             |

***

## Index Fields

Available Index Fields:

| Name              | Description |
|:------------------|:------------|
|`binary`           | Binary fields are not tokenized or indexed, but are stored for retrieval with search hits. They can be used to store any data encoded as a binary string, such as an image icon. |
|`keyword`          | Keyword fields are stored and indexed, meaning that they can be searched as well as displayed in search results. They are not split up into separate words by tokenization. |
|`text`             | Text fields are stored, indexed, and tokenized. Text fields are appropriate for storing information like subjects and titles that need to be searchable as well as returned with search results. |
|`unIndexed`        | UnIndexed fields are not searchable, but they are returned with search hits. Database timestamps, primary keys, file system paths, and other external identifiers are good candidates for UnIndexed fields. |
|`unStored`         | UnStored fields are tokenized and indexed, but not stored in the index. Large amounts of text are best indexed using this type of field. Storing data creates a larger index on disk, so if you need to search but not redisplay the data, use an UnStored field.|

***

## OutputChannel

### Autocomplete

Available Options:

| Name                             | Default Value | Description |
|:---------------------------------|:--------------|:------------|
|`min_prefix_length`               | 3             |             |
|`use_fuzzy_term_search_fallback`  | true          |             |
|`fuzzy_default_prefix_length`     |               |             |
|`fuzzy_similarity`                | 0.5           |             |

### Suggestions

Available Options:

| Name                             | Default Value | Description |
|:---------------------------------|:--------------|:------------|
|`min_prefix_length`               | 3             |             |
|`result_limit`                    | 10            |             |
|`only_last_word_wildcard`         | false         |             |
|`multiple_words_operator`         | 'OR'          |             |
|`restrict_search_fields`          | []            |             |
|`restrict_search_fields_operator` | 'OR'          |             |

### Search

Available Options:

| Name                             | Default Value | Description |
|:---------------------------------|:--------------|:------------|
|`min_prefix_length`               | 3             |             |
|`max_per_page`                    | 10            |             |

***

## Output Normalizer

A Output Normalizer can be defined for each output channel.

### lucene_document_key_value_normalizer

Available Options:

| Name                       | Default Value | Description |
|----------------------------|---------------|-------------|
|`skip_fields`               | []            |             |
