<h1 align="center">Charset Detection, for Everyone 👋 <a href="https://twitter.com/intent/tweet?text=The%20Real%20First%20Universal%20Charset%20%26%20Language%20Detector&url=https://www.github.com/Ousret/charset_normalizer&hashtags=python,encoding,chardet,developers"><img src="https://img.shields.io/twitter/url/http/shields.io.svg?style=social"/></a></h1>

<p align="center">
  <sup>The Real First Universal Charset Detector</sup><br>
  <a href="https://travis-ci.org/Ousret/charset_normalizer">
    <img src="https://travis-ci.org/Ousret/charset_normalizer.svg?branch=master"/>
  </a>
  <a href="https://pypi.org/project/charset-normalizer">
    <img src="https://img.shields.io/pypi/pyversions/charset_normalizer.svg?orange=blue" />
  </a>
  <a href="https://app.codacy.com/project/Ousret/charset_normalizer/dashboard">
    <img alt="Code Quality Badge" src="https://api.codacy.com/project/badge/Grade/a0c85b7f56dd4f628dc022763f82762c"/>
  </a>
  <a href="https://codecov.io/gh/Ousret/charset_normalizer">
      <img src="https://codecov.io/gh/Ousret/charset_normalizer/branch/master/graph/badge.svg" />
  </a>
  <a href='https://charset-normalizer.readthedocs.io/en/latest/?badge=latest'>
    <img src='https://readthedocs.org/projects/charset-normalizer/badge/?version=latest' alt='Documentation Status' />
  </a>
  <a href="https://pepy.tech/project/charset-normalizer/">
    <img alt="Download Count Total" src="https://pepy.tech/badge/charset-normalizer" />
  </a>
</p>

> A library that helps you read text from an unknown charset encoding.<br /> Motivated by `chardet`,
> I'm trying to resolve the issue by taking a new approach.
> All IANA character set names for which the Python core library provides codecs are supported.

<p align="center">
  >>>>> <a href="https://charsetnormalizerweb.ousret.now.sh" target="_blank">👉 Try Me Online Now, Then Adopt Me 👈 </a> <<<<<
</p>

This project offers you an alternative to **Universal Charset Encoding Detector**, also known as **Chardet**.

| Feature       | [Chardet](https://github.com/chardet/chardet)       | Charset Normalizer | [cChardet](https://github.com/PyYoshi/cChardet) |
| ------------- | :-------------: | :------------------: | :------------------: |
| `Fast`         | ❌<br>          | :heavy_check_mark:<br>             | :heavy_check_mark: <br> |
| `Universal**`     | ❌            | :heavy_check_mark:                 | ❌ |
| `Reliable` **without** distinguishable standards | ❌ | :heavy_check_mark: | :heavy_check_mark: |
| `Reliable` **with** distinguishable standards | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| `Free & Open`  | :heavy_check_mark:             | :heavy_check_mark:                | :heavy_check_mark: |
| `License` | LGPL-2.1 | MIT | MPL-1.1
| `Native Python` | :heavy_check_mark: | :heavy_check_mark: | ❌ |
| `Detect spoken language` | ❌ | :heavy_check_mark: | N/A |
| `Supported Encoding` | 30 | :tada: [93](https://charset-normalizer.readthedocs.io/en/latest/support.html)  | 40

<p align="center">
<img src="https://i.imgflip.com/373iay.gif" alt="Reading Normalized Text" width="226"/><img src="https://media.tenor.com/images/c0180f70732a18b4965448d33adba3d0/tenor.gif" alt="Cat Reading Text" width="200"/>

*\*\* : They are clearly using specific code for a specific encoding even if covering most of used one*<br> 

## ⚡ Performance

This package offer better performance than its counterpart Chardet. Here are some numbers.

| Package       | Accuracy       | Mean per file (ns) | File per sec (est) |
| ------------- | :-------------: | :------------------: | :------------------: |
|      [chardet](https://github.com/chardet/chardet)        |     93.0 %     |     67 ms      |       15.38 file/sec        |
| charset-normalizer |    **95.0 %**     |     **37 ms**      |       27.77 file/sec    |

| Package       | 99th percentile       | 95th percentile | 50th percentile |
| ------------- | :-------------: | :------------------: | :------------------: |
|      [chardet](https://github.com/chardet/chardet)        |     424 ms     |     234 ms      |       26 ms        |
| charset-normalizer |    335 ms     |     186 ms      |       17 ms    |

Chardet's performance on larger file (1MB+) are very poor. Expect huge difference on large payload.

> Stats are generated using 400+ files using default parameters. More details on used files, see GHA workflows.
> And yes, these results might change at any time. The dataset can be updated to include more files.

[cchardet](https://github.com/PyYoshi/cChardet) is a non-native (cpp binding) faster alternative. If speed is the most important factor,
you should try it.

## Your support

Please ⭐ this repository if this project helped you!

## ✨ Installation

Using PyPi for latest stable
```sh
pip install charset-normalizer
```
Or directly from dev-master for latest preview
```sh
pip install git+https://github.com/Ousret/charset_normalizer.git
```

If you want a more up-to-date `unicodedata` than the one available in your Python setup.
```sh
pip install charset-normalizer[unicode_backport]
```

## 🚀 Basic Usage

### CLI
This package comes with a CLI.

```
usage: normalizer [-h] [-v] [-a] [-n] [-m] [-r] [-f] [-t THRESHOLD]
                  file [file ...]

The Real First Universal Charset Detector. Discover originating encoding used
on text file. Normalize text to unicode.

positional arguments:
  files                 File(s) to be analysed

optional arguments:
  -h, --help            show this help message and exit
  -v, --verbose         Display complementary information about file if any.
                        Stdout will contain logs about the detection process.
  -a, --with-alternative
                        Output complementary possibilities if any. Top-level
                        JSON WILL be a list.
  -n, --normalize       Permit to normalize input file. If not set, program
                        does not write anything.
  -m, --minimal         Only output the charset detected to STDOUT. Disabling
                        JSON output.
  -r, --replace         Replace file when trying to normalize it instead of
                        creating a new one.
  -f, --force           Replace file without asking if you are sure, use this
                        flag with caution.
  -t THRESHOLD, --threshold THRESHOLD
                        Define a custom maximum amount of chaos allowed in
                        decoded content. 0. <= chaos <= 1.
  --version             Show version information and exit.
```

```bash
normalizer ./data/sample.1.fr.srt
```

:tada: Since version 1.4.0 the CLI produce easily usable stdout result in JSON format.

```json
{
    "path": "/home/default/projects/charset_normalizer/data/sample.1.fr.srt",
    "encoding": "cp1252",
    "encoding_aliases": [
        "1252",
        "windows_1252"
    ],
    "alternative_encodings": [
        "cp1254",
        "cp1256",
        "cp1258",
        "iso8859_14",
        "iso8859_15",
        "iso8859_16",
        "iso8859_3",
        "iso8859_9",
        "latin_1",
        "mbcs"
    ],
    "language": "French",
    "alphabets": [
        "Basic Latin",
        "Latin-1 Supplement"
    ],
    "has_sig_or_bom": false,
    "chaos": 0.149,
    "coherence": 97.152,
    "unicode_path": null,
    "is_preferred": true
}
```

### Python
*Just print out normalized text*
```python
from charset_normalizer import from_path

results = from_path('./my_subtitle.srt')

print(str(results.best()))
```

*Normalize any text file*
```python
from charset_normalizer import normalize
try:
    normalize('./my_subtitle.srt') # should write to disk my_subtitle-***.srt
except IOError as e:
    print('Sadly, we are unable to perform charset normalization.', str(e))
```

*Upgrade your code without effort*
```python
from charset_normalizer import detect
```

The above code will behave the same as **chardet**. We ensure that we offer the best (reasonable) BC result possible.

See the docs for advanced usage : [readthedocs.io](https://charset-normalizer.readthedocs.io/en/latest/)

## 😇 Why

When I started using Chardet, I noticed that it was not suited to my expectations, and I wanted to propose a
reliable alternative using a completely different method. Also! I never back down on a good challenge !

I **don't care** about the **originating charset** encoding, because **two different tables** can
produce **two identical files.**
What I want is to get readable text, the best I can. 

In a way, **I'm brute forcing text decoding.** How cool is that ? 😎

Don't confuse package **ftfy** with charset-normalizer or chardet. ftfy goal is to repair unicode string whereas charset-normalizer to convert raw file in unknown encoding to unicode.

## 🍰 How

  - Discard all charset encoding table that could not fit the binary content.
  - Measure chaos, or the mess once opened (by chunks) with a corresponding charset encoding.
  - Extract matches with the lowest mess detected.
  - Finally, if there is too much match left, we measure coherence.

**Wait a minute**, what is chaos/mess and coherence according to **YOU ?**

*Chaos :* I opened hundred of text files, **written by humans**, with the wrong encoding table. **I observed**, then
**I established** some ground rules about **what is obvious** when **it seems like** a mess.
 I know that my interpretation of what is chaotic is very subjective, feel free to contribute in order to
 improve or rewrite it.

*Coherence :* For each language there is on earth, we have computed ranked letter appearance occurrences (the best we can). So I thought
that intel is worth something here. So I use those records against decoded text to check if I can detect intelligent design.

## ⚡ Known limitations

  - Language detection is unreliable when text contains two or more languages sharing identical letters. (eg. HTML (english tags) + Turkish content (Sharing Latin characters))
  - Every charset detector heavily depends on sufficient content. In common cases, do not bother run detection on very tiny content.

## 👤 Contributing

Contributions, issues and feature requests are very much welcome.<br />
Feel free to check [issues page](https://github.com/ousret/charset_normalizer/issues) if you want to contribute.

## 📝 License

Copyright © 2019 [Ahmed TAHRI @Ousret](https://github.com/Ousret).<br />
This project is [MIT](https://github.com/Ousret/charset_normalizer/blob/master/LICENSE) licensed.

Characters frequencies used in this project © 2012 [Denny Vrandečić](http://denny.vrandecic.de)
