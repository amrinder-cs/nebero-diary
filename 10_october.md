# 10th October Diary

- Added logging to find out which sort of data causes the error in the socket stream.
- Ran the program in production to find out exactly where the issue arises. It was found that the socket wasn't sending the data yet, and my program was reading it earlier, causing some bytes to be skipped. These further caused issues upon loop repetition.
- Fixed the aforementioned bug and made the length processing function resilient to bad data. This means it will just ignore the dirty data and process only the required data.
- The logging function now auto-appends the date, making it slightly better for logging. By default, it only logs; for verbose logs, use the `-d` option.
- Made it so the program loops until it has received sufficient data, instead of erroring when the data isn't yet received.