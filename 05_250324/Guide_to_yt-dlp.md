# Guide to using `yt-dlp`
This document contains the "plain-text" version of the commands needed to use `yt-dlp`, since text/commands copied from the slides in PDF format may result in errors (beside the mistakes I made while writing the commands in the slide).  
***All commands are on one single line (i.e. there must be no newlines in the text you input in the terminal)***: the commands included in this document should be copy-paste-safe, and should not produced text split with newlines when copied.

***NOTE***: `yt-dlp` saves the data inside the folder currently open in the terminal, which for both Windows and macOS is the `User` folder (so, for the username mdicristofaro `yt-dlp` saves the data inside `C:/Users/mdicristofaro/` on Windows). Assuming you have created a folder called `youtube` inside the `Downloads` folder, once the terminal is open you may type the following command to enter inside the `Downloads/youtube` folder:

> **Windows**  
`cd Downloads\youtube`
  
> **macOS**  
`cd Downloads/youtube`

## Downloading subtitles and metadata for one single video (URL)
The general syntax is as follows:  

> `yt-dlp "URL" --write-info-json --skip-download --write-subs --write-auto-subs --sub-langs [LL] --sub-format srv3`

where **you must replace `URL` and `[LL]`** with the link to the video and the label of the language of the subtitles respectively (see below for getting the language label from the video). So, for the video [The underground cities of the Byzantine Empire - Veronica Kalas](https://www.youtube.com/watch?v=zs-zATBh_Ho) the command would be:

> `yt-dlp "https://www.youtube.com/watch?v=zs-zATBh_Ho" --write-info-json --skip-download --write-subs --write-auto-subs --sub-langs en --sub-format srv3`

## Downloading subtitles and metadata for a list of videos (URLs)

Assuming you have saved a number of links inside of a `.txt` file, with one link per line as exemplified below:

> https://www.youtube.com/watch?v=zs-zATBh_Ho  
https://www.youtube.com/watch?v=Z8dZSySRX_g  
https://www.youtube.com/watch?v=BhcGvBxSBEA

the following command processes the `.txt` file and downloads data for each video

> `yt-dlp -a LIST_OF_URL.txt --write-info-json --skip-download --write-subs --write-auto-subs --sub-langs [LL] --sub-format srv3`

where **you must replace `LIST_OF_URL.txt` and `[LL]`** with the name of the `.txt` file containing the links and the label of the language of the subtitles respectively (see below for getting the language label from the video).

## Downloading subtitles and metadata for a list of videos (URLs) *skipping already downloaded subtitles*
Assuming that the list of links you have collected contains (or may contain) duplicate links, the following command processes the list while writing a list of the ones already downloaded (`archive.txt`), so that the latter can be skipped while collecting the data

> `yt-dlp -a LIST_OF_URL.txt --force-write-archive --download-archive archive.txt --write-info-json --skip-download --write-subs --write-auto-subs --sub-langs [LL] --sub-format srv3`

## Identifying the language label for a video subtitles
The general syntax is as follows:

> `yt-dlp --list-subs "URL"`

where **you must replace `URL`** with the link to the video. So, for the video [The underground cities of the Byzantine Empire - Veronica Kalas](https://www.youtube.com/watch?v=zs-zATBh_Ho) the command would be:

> `yt-dlp --list-subs "https://www.youtube.com/watch?v=zs-zATBh_Ho"`

which will output a huge list of languages in the terminal, following the structure below (I have only included a limited number of lines from the output):

```
Language   Name                                  Formats
ar                                               vtt
en                                               vtt
fr                                               vtt
id                                               vtt
it                                               vtt
af-ar      Afrikaans from Arabic                 vtt, ttml, srv3, srv2, srv1, json3
ak-ar      Akan from Arabic                      vtt, ttml, srv3, srv2, srv1, json3

...

yi-it      Yiddish from Italian                  vtt, ttml, srv3, srv2, srv1, json3
yo-it      Yoruba from Italian                   vtt, ttml, srv3, srv2, srv1, json3
zu-it      Zulu from Italian                     vtt, ttml, srv3, srv2, srv1, json3
[info] Available subtitles for zs-zATBh_Ho:
Language Name       Formats
ar       Arabic     vtt, ttml, srv3, srv2, srv1, json3
en       English    vtt, ttml, srv3, srv2, srv1, json3
fr       French     vtt, ttml, srv3, srv2, srv1, json3
id       Indonesian vtt, ttml, srv3, srv2, srv1, json3
it       Italian    vtt, ttml, srv3, srv2, srv1, json3


```

The output has three columns, and the label may be found in the first one (`Language`); also notice that, since we want to download the subtitles in `.srv3` format, you need to verify that the format is listed in the third column (`Formats`) for the label/language you want to download.
