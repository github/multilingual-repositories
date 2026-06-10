# GitHub Multilingual Repositories Dataset

## Dataset Summary

The GitHub Multilingual Repositories Dataset is a repository-level metadata dataset intended to help researchers find GitHub repositories with evidence of non-English natural-language content. It contains language-classification signals derived from repository README files, issues, and pull requests, plus repository metadata such as creation timestamp, disk usage, stars, forks, primary programming language, SPDX license, issue counts, pull request counts, and snapshot date.

The current prepared classification data contains 80,657,333 classification rows across 40,817,528 distinct repositories. Language classifications are produced by three language-identification systems: [fastText](https://fasttext.cc/), [gcld3](https://github.com/google/cld3), and [lingua-py](https://github.com/pemistahl/lingua-py).

This dataset does not aim to provide a definitive language label for every repository. Instead, it exposes multiple classifier outputs and confidence scores so users can choose their own precision/recall tradeoff, such as requiring two or three classifiers to agree on a language before including a repository.

## Dataset Details

### Dataset Description

- **Repository:** https://github.com/github/multilingual-repositories
- **Point of contact:** policy@github.com
- **License:** CC0-1.0

### Dataset Sources

The dataset was prepared from public GitHub repository data, including README files, issue text, pull request text, and repository metadata.

## Uses

### Direct Use

This dataset is intended for research workflows that need to discover GitHub repositories likely to contain natural-language content in specific languages. Example uses include:

- selecting repositories for multilingual software-engineering research;
- estimating the prevalence of non-English README, issue, or pull request content on GitHub;
- analyzing repository-level metadata distributions, such as stars, repository size, primary programming language, issue counts, pull request counts, or SPDX licenses, across language-classified repositories.

### Out-of-Scope Use

This dataset should not be used as a ground-truth benchmark for language identification. Labels are automatically inferred from short text snippets and may be wrong, especially for short, boilerplate, code-heavy, mixed-language, or low-resource-language content.

This dataset should also not be used to infer sensitive attributes about repository owners, contributors, or communities. Language signals are repository-level metadata, not person-level attributes.

### `repository_classifications`

One row per repository/classification signal.

| Column | Type | Description |
| --- | --- | --- |
| `repository_id` | int64 | GitHub repository identifier. |
| `lang_code` | string | Detected ISO 639 language code, stored as an uppercase code in prepared artifacts. |
| `confidence` | float64 | Classifier confidence score. Interpretability varies by classifier. |
| `source` | string | Text source used for classification: `readme`, `issue`, or `pull_request`. |
| `classifier` | string | Classifier that produced the prediction: `fasttext`, `gcld3`, or `linguapy`. |

Current row counts by source:

| Source | Rows |
| --- | ---: |
| `readme` | 66,177,034 |
| `issue` | 4,756,279 |
| `pull_request` | 9,724,020 |

Current row counts by classifier:

| Classifier | Rows |
| --- | ---: |
| `fasttext` | 25,909,973 |
| `gcld3` | 34,441,896 |
| `linguapy` | 20,305,464 |

### `repo_metadata`

One row per repository.

| Column | Type | Description |
| --- | --- | --- |
| `repository_id` | int64 | GitHub repository identifier. |
| `disk_usage_bytes` | int64 | Repository disk usage in bytes. |
| `num_public_forks` | int64 | Number of public forks. |
| `num_stars` | int64 | Number of stars. |
| `created_at` | timestamp | Repository creation timestamp. |
| `primary_language_name` | string | Primary programming language name from repository metadata. |
| `spdx_license` | string | SPDX license identifier from repository metadata, if available. |
| `num_pull_requests` | int64 | Number of pull requests. |
| `num_issues` | int64 | Number of issues. |
| `snapshot_day` | date | Metadata snapshot date. |

### Aggregate Statistics

#### Where a language was detected in a readme by at least two classifiers with > 0.5 confidence

| lang_code | count_distinct_repos | sum_disk_usage_bytes | sum_pull_requests | sum_issues | sum_stars |
| --- | ---: | ---: | ---: | ---: | ---: |
| PT | 3039349 | 18634870231 | 2923341 | 654793 | 1093458 |
| ES | 2136023 | 20511334099 | 2098640 | 527660 | 465748 |
| RU | 1436777 | 10602026479 | 1747173 | 321766 | 609679 |
| FR | 813898 | 10548579163 | 1307626 | 389468 | 213967 |
| KO | 678744 | 15266316578 | 2496294 | 794141 | 427186 |
| TR | 265927 | 2457800378 | 110796 | 26214 | 196800 |
| ID | 259280 | 2042514982 | 175442 | 22819 | 71868 |
| ZH | 221516 | 2424344181 | 150279 | 78355 | 1307257 |
| DE | 218534 | 3399949387 | 433184 | 225940 | 113963 |
| VI | 213848 | 4098899955 | 348004 | 46438 | 85766 |
| JA | 166852 | 1955644319 | 720076 | 240974 | 121484 |
| PL | 153784 | 1720316080 | 222612 | 61696 | 41437 |
| IT | 141284 | 1865652471 | 144021 | 80654 | 43582 |
| UK | 121157 | 873045659 | 177227 | 15448 | 21141 |
| NL | 85902 | 1264777557 | 175878 | 86890 | 14397 |
| CS | 49004 | 601745632 | 66340 | 36667 | 16188 |
| TH | 47608 | 478888884 | 34559 | 12524 | 13231 |
| HU | 39823 | 418171210 | 45838 | 24821 | 8558 |
| SV | 39303 | 338601401 | 95238 | 34526 | 7117 |
| RO | 38858 | 631958921 | 32553 | 13727 | 7536 |
| FI | 27590 | 195495894 | 74818 | 37468 | 4179 |
| CA | 18771 | 311674134 | 20676 | 9804 | 3363 |
| DA | 14844 | 206281594 | 30480 | 16107 | 3792 |
| SK | 10902 | 164620091 | 18271 | 8291 | 3786 |
| EL | 10732 | 114289938 | 15491 | 4265 | 4160 |
| LT | 8714 | 92533405 | 14759 | 1466 | 1179 |
| ET | 8093 | 71612416 | 11107 | 7599 | 1056 |
| BG | 7832 | 103318662 | 12040 | 3072 | 7088 |
| SL | 7124 | 112800880 | 7035 | 3496 | 1799 |
| IS | 6936 | 75730073 | 11518 | 2440 | 944 |
| BN | 6923 | 23496141 | 3402 | 647 | 10184 |
| BS | 4947 | 80169196 | 6389 | 1497 | 1196 |
| KA | 4799 | 25695939 | 4760 | 7960 | 708 |
| HR | 3677 | 51418034 | 4007 | 2479 | 742 |
| MK | 2832 | 38667420 | 2914 | 327 | 558 |
| CY | 2752 | 24587891 | 2060 | 513 | 499 |
| EU | 2667 | 33104272 | 1427 | 1564 | 513 |
| KK | 1581 | 6343259 | 188 | 40 | 184 |
| HI | 1237 | 8787540 | 118 | 59 | 153 |
| XH | 960 | 9898724 | 90 | 69 | 82 |
| SO | 767 | 1596992 | 362 | 107 | 194 |
| MY | 611 | 6243830 | 519 | 63 | 2145 |
| HY | 593 | 4661614 | 976 | 87 | 208 |
| SR | 474 | 6740598 | 1280 | 296 | 220 |
| EO | 377 | 4736974 | 471 | 682 | 688 |
| TA | 258 | 8727603 | 750 | 905 | 328 |
| BE | 234 | 14522442 | 891 | 663 | 574 |
| UR | 223 | 2725122 | 30 | 16 | 50 |
| AF | 151 | 608384 | 22 | 13 | 32 |
| MR | 144 | 1231972 | 24 | 26 | 31 |
| ZU | 118 | 458095 | 11 | 0 | 5 |
| SN | 85 | 94718 | 12 | 2 | 6 |
| GA | 83 | 884001 | 87 | 44 | 169 |
| TE | 81 | 76971 | 40 | 11 | 7 |
| GU | 58 | 314934 | 87 | 39 | 23 |
| AR | 31 | 142170 | 24 | 2 | 21 |
| FA | 27 | 319787 | 195 | 48 | 151 |
| MI | 26 | 159222 | 9 | 60 | 56 |
| PA | 20 | 751508 | 151 | 2 | 6 |
| ST | 12 | 78391 | 1 | 0 | 0 |
| LV | 10 | 3904 | 1 | 0 | 1 |
| MS | 8 | 262524 | 0 | 0 | 4 |
| GL | 8 | 24505 | 0 | 0 | 1 |
| HE | 7 | 1419 | 0 | 0 | 1 |
| LA | 5 | 4098 | 0 | 0 | 0 |
| NB | 5 | 178820 | 3 | 0 | 1 |
| SQ | 4 | 121103 | 1 | 2 | 0 |
| NE | 3 | 14235 | 0 | 0 | 0 |
| NO | 3 | 23141 | 8 | 0 | 0 |
| AZ | 3 | 1122 | 0 | 0 | 11 |
| YO | 2 | 2 | 0 | 0 | 0 |
| TG | 2 | 266 | 1 | 0 | 0 |
| MN | 2 | 437 | 0 | 0 | 0 |
| LB | 1 | 2520 | 0 | 0 | 0 |
| HA | 1 | 436 | 0 | 0 | 0 |
| JV | 1 | 14059 | 8 | 0 | 0 |
| CE | 1 | 2874 | 0 | 0 | 1 |

#### Where a language was detected in an Issue by at least two classifiers with > 0.5 confidence

| lang_code | count_distinct_repos | sum_disk_usage_bytes | sum_pull_requests | sum_issues | sum_stars |
| --- | ---: | ---: | ---: | ---: | ---: |
| KO | 127993 | 3309240944 | 2976499 | 2082628 | 577165 |
| ES | 116139 | 2338966908 | 920154 | 1174768 | 537262 |
| PT | 112244 | 2040665888 | 1084182 | 1151211 | 830842 |
| RU | 111634 | 1888185183 | 1014984 | 1023016 | 932307 |
| JA | 86087 | 1333986260 | 1648070 | 937384 | 319068 |
| FR | 64604 | 1952155525 | 1130792 | 966295 | 266327 |
| ZH | 47820 | 1157213252 | 276045 | 395168 | 5010214 |
| DE | 38046 | 1303760686 | 674594 | 699728 | 170550 |
| NL | 16035 | 431178429 | 204824 | 259415 | 17157 |
| PL | 14191 | 381589271 | 160265 | 185762 | 35171 |
| VI | 12165 | 309141122 | 116608 | 111972 | 58073 |
| IT | 11466 | 425440901 | 129400 | 175481 | 50663 |
| TR | 9747 | 174730865 | 73943 | 70806 | 100957 |
| ID | 7982 | 127763739 | 59781 | 51102 | 83633 |
| CS | 6555 | 187599440 | 92358 | 86368 | 15952 |
| FI | 6301 | 95283622 | 43946 | 67144 | 3305 |
| UK | 5355 | 93600606 | 60911 | 49288 | 12223 |
| SV | 5147 | 91786119 | 71881 | 82874 | 7645 |
| HU | 3934 | 95989677 | 32226 | 46285 | 6130 |
| TH | 3398 | 36986043 | 27631 | 30800 | 63750 |
| RO | 2516 | 51040437 | 16076 | 28905 | 3959 |
| DA | 2166 | 57037914 | 31263 | 45981 | 3787 |
| SL | 1858 | 18962287 | 4391 | 8665 | 1308 |
| CY | 1523 | 11913563 | 6760 | 5106 | 1602 |
| SK | 1472 | 31054229 | 26251 | 22058 | 8573 |
| CA | 1449 | 45967520 | 14761 | 28712 | 2160 |
| EL | 888 | 18862688 | 11248 | 9353 | 2964 |
| ET | 848 | 17309584 | 4880 | 12130 | 582 |
| BG | 745 | 16583881 | 8147 | 8638 | 3770 |
| LT | 621 | 13792374 | 8375 | 7323 | 1085 |
| KA | 545 | 5401721 | 3243 | 5105 | 568 |
| IS | 458 | 10603625 | 4277 | 4103 | 584 |
| BS | 369 | 8694470 | 3578 | 4146 | 260 |
| HR | 289 | 5453396 | 2377 | 2891 | 1072 |
| EU | 252 | 3748737 | 1710 | 3600 | 475 |
| BN | 176 | 7786383 | 649 | 850 | 1586 |
| BE | 94 | 14710936 | 1290 | 2107 | 503 |
| EO | 89 | 2248514 | 1295 | 1270 | 569 |
| HY | 77 | 254106 | 298 | 249 | 62 |
| SO | 75 | 231471 | 375 | 241 | 34 |
| HI | 68 | 719827 | 86 | 189 | 56 |
| MK | 67 | 1063640 | 300 | 860 | 167 |
| KK | 59 | 89135 | 60 | 126 | 128 |
| MY | 55 | 257502 | 293 | 219 | 334 |
| SR | 39 | 1127400 | 379 | 474 | 427 |
| TA | 33 | 536405 | 79 | 1213 | 357 |
| AF | 21 | 37886 | 9 | 52 | 23 |
| UR | 15 | 9273 | 1 | 761 | 3 |
| GA | 11 | 162930 | 77 | 51 | 54 |
| TE | 9 | 8523 | 6 | 41 | 52 |
| GU | 8 | 12043 | 35 | 765 | 7 |
| PA | 5 | 2568 | 26 | 25 | 6 |
| MR | 4 | 152 | 0 | 12 | 0 |
| XH | 4 | 56 | 0 | 7 | 0 |
| SN | 4 | 5644 | 2 | 8 | 4 |
| ZU | 3 | 29 | 0 | 3 | 0 |

#### Where a language was detected in a Pull Request by at least two classifiers with > 0.5 confidence

| lang_code | count_distinct_repos | sum_disk_usage_bytes | sum_pull_requests | sum_issues | sum_stars |
| --- | ---: | ---: | ---: | ---: | ---: |
| ES | 184868 | 3042601320 | 1774806 | 373078 | 302039 |
| KO | 166734 | 5038064201 | 4486282 | 1542530 | 459962 |
| PT | 157804 | 4510822023 | 1586629 | 485067 | 704488 |
| RU | 153260 | 2517982339 | 1698917 | 402631 | 588555 |
| JA | 97110 | 1396376696 | 1477459 | 437531 | 264518 |
| FR | 82750 | 2250909133 | 1450917 | 402318 | 184542 |
| DE | 30839 | 924572644 | 510166 | 260078 | 129538 |
| PL | 17307 | 362718954 | 214214 | 90995 | 38564 |
| NL | 15928 | 348003130 | 229139 | 95532 | 23081 |
| ZH | 12019 | 286579355 | 130122 | 104173 | 2005294 |
| ID | 11412 | 143260276 | 97330 | 22437 | 32427 |
| IT | 9905 | 387813064 | 126978 | 67236 | 32036 |
| TR | 9640 | 186472857 | 95307 | 24650 | 92021 |
| VI | 9232 | 235299837 | 149566 | 15757 | 19622 |
| UK | 6344 | 83038753 | 131532 | 9079 | 8411 |
| CY | 6246 | 118689296 | 40767 | 5500 | 19033 |
| CS | 4425 | 88884358 | 80674 | 33913 | 11116 |
| SV | 4178 | 83000678 | 66090 | 25730 | 5626 |
| HU | 3141 | 47457203 | 36586 | 19424 | 4193 |
| FI | 3005 | 92846230 | 80090 | 15968 | 2779 |
| RO | 2708 | 64689361 | 30812 | 8415 | 2983 |
| TH | 2370 | 53543483 | 30660 | 3823 | 7217 |
| DA | 1992 | 48110221 | 30092 | 13384 | 3379 |
| CA | 1424 | 39623026 | 17273 | 6328 | 1299 |
| SK | 1279 | 34894256 | 21727 | 9862 | 2114 |
| SL | 912 | 9644404 | 4927 | 2232 | 705 |
| LT | 859 | 13014940 | 10942 | 2108 | 783 |
| EL | 765 | 24665530 | 14737 | 7446 | 2055 |
| IS | 760 | 8492954 | 9390 | 1656 | 474 |
| EU | 671 | 21236398 | 3288 | 593 | 362 |
| ET | 619 | 9140611 | 6699 | 2949 | 381 |
| BG | 466 | 8035684 | 6465 | 2062 | 3586 |
| KA | 463 | 5467080 | 6553 | 946 | 289 |
| HR | 350 | 5697021 | 3389 | 611 | 280 |
| BS | 322 | 5387952 | 4708 | 949 | 1048 |
| MK | 109 | 1531300 | 897 | 133 | 90 |
| BN | 80 | 294764 | 276 | 228 | 4356 |
| HY | 79 | 1796868 | 1438 | 168 | 96 |
| SO | 79 | 457989 | 686 | 31 | 109 |
| EO | 73 | 990840 | 1644 | 785 | 484 |
| BE | 67 | 1347384 | 618 | 406 | 252 |
| YO | 54 | 58714 | 80 | 0 | 0 |
| AF | 38 | 244773 | 113 | 31 | 15 |
| KK | 35 | 36048 | 135 | 18 | 57 |
| HI | 30 | 270207 | 47 | 1 | 3 |
| GA | 28 | 697888 | 127 | 45 | 49 |
| SR | 26 | 497360 | 312 | 74 | 38 |
| MY | 19 | 1053472 | 380 | 22 | 192 |
| TA | 15 | 214589 | 245 | 9 | 76 |
| SN | 9 | 33154 | 16 | 0 | 3 |
| UR | 8 | 85054 | 9 | 0 | 2 |
| ZU | 4 | 254 | 7 | 0 | 2 |
| XH | 3 | 3236 | 11 | 0 | 0 |
| TE | 3 | 113041 | 11 | 0 | 0 |
| MR | 3 | 24981 | 6 | 1 | 7 |
| PA | 2 | 58 | 2 | 0 | 5 |
| ST | 2 | 43874 | 2 | 0 | 0 |
| MI | 2 | 7400 | 133 | 2 | 0 |
| GU | 1 | 18 | 1 | 2 | 5 |

## Dataset Creation

### Curation Rationale

The dataset was created to make it easier to identify repositories containing multilingual natural-language developer content. The motivation is not to compete with broad web-scale text corpora on token volume, but to expose developer-centric content signals from README files, issues, and pull requests.

### Source Data

Repositories were classified by the spoken language of text found in README files, issues, and pull requests.

- **Root READMEs:** the first 150 characters of each repository's root `README.md`, matched case-insensitively, were used for language detection. READMEs with fewer than 20 characters were excluded from classification.
- **Issues and pull requests:** for each repository, issues and pull requests were filtered to records with at least 20 characters in the `body` field. The issue or pull request with the most comments per repository was selected, and the first 150 characters of the concatenated title, body, and comments were used for classification.

### Language Classification

Each selected text sample was classified with fastText, gcld3, and lingua-py, and only observations where the classifier detected a non-English language with confidence greater than 0.5 were included in the prepared dataset.

## Biases, Risks, and Limitations

Language labels are inferred from very short snippets. A 150-character prefix may capture badges, templates, installation commands, issue boilerplate, code fragments, usernames, or mixed-language text rather than representative prose.

The issue and pull request sampling strategy intentionally selects the most-commented issue or pull request per repository after filtering, which may overrepresent contentious, popular, or support-heavy discussions and underrepresent typical repository activity.

Classifier coverage and calibration differ across fastText, gcld3, and lingua-py. Confidence scores should not be assumed to be directly comparable across classifiers, and users should consider requiring agreement among multiple classifiers for high-precision use cases.

Repository metadata is a snapshot and may become stale as repositories are deleted, archived, transferred, or otherwise updated.

## Citation

```bibtex
@misc{
  title = {GitHub Multilingual Repositories Dataset: Repository-Level Language Classifications and Metadata for GitHub Repositories},
  author = {GitHub, Inc.},
  year = {2026},
  publisher = {GitHub, Inc.},
  url = {github/multilingual-repositories}
}
```
