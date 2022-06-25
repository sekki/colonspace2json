# colonspace2json
文字列の区切りはコロンで、一節の区切りは空白区切りのテキストデータをjsonに変換するやつ。

もともとは ``` ipmitool sel elist ``` の結果をjsonで見たいために作りました。  


例）
```
$ cat test.txt 
hoge : fuga
piyo : nya-

foo : bar

$ cat test.txt | ./cs2json | jq "."
[
  {
    "piyo": "nya-",
    "hoge": "fuga"
  },
  {
    "foo": "bar"
  }
]

```


例)
```
$ ipmitool -I lanplus -H "${BMC_IP}" -U admin -P admin -v sel elist | ./cs2json
[{"Sensor Number": "00", "Generator ID": "0041", "SEL Record ID": "00a9", "Sensor Type": "OS Boot", "Timestamp": "05/21/2018 03:02:24", "Event Data": "01ffff", "Event Direction": "Assertion Event", "Record Type": "02", "EvM Revision": "04", "Event Type": "Sensor-specific Discrete", "Description": "C: boot completed"}, 
(..snip..)
```

例)
```
$ cat sel_elist-v/PRIMERGY_TX1320_M2-1.txt | ./cs2json 
[{"Sensor Number": "64", "Generator ID": "0020", "SEL Record ID": "000a", "Sensor Type": "System ACPI Power State", "Timestamp": "05/16/2016 14:37:17", "Event Data": "0affff", "Event Direction": "Assertion Event", "Record Type": "02", "EvM Revision": "04", "Event Type": "Sensor-specific Discrete", "Description": "S5: entered by override"}, 
(..snip..)
```

