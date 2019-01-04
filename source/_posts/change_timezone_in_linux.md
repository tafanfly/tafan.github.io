title: Linux下更改时区

categories: Linux

tags:
  - timezone

---
#### tzselect
tzselect 该命令可以查询时区并生成配置信息，并不会实际生效。
举例说明需要配置中国北京时间， 则按照步骤一步步选择下去，得到配置信息为`TZ='Asia/Shanghai'; export TZ`
<!-- more -->
```
tafan ~ $ tzselect
Please identify a location so that time zone rules can be set correctly.
Please select a continent, ocean, "coord", or "TZ".
 1) Africa
 2) Americas
 3) Antarctica
 4) Asia
 5) Atlantic Ocean
 6) Australia
 7) Europe
 8) Indian Ocean
 9) Pacific Ocean
10) coord - I want to use geographical coordinates.
11) TZ - I want to specify the time zone using the Posix TZ format.
#? 4
Please select a country whose clocks agree with yours.
 1) Afghanistan           18) Israel                35) Palestine
 2) Armenia               19) Japan                 36) Philippines
 3) Azerbaijan            20) Jordan                37) Qatar
 4) Bahrain               21) Kazakhstan            38) Russia
 5) Bangladesh            22) Korea (North)         39) Saudi Arabia
 6) Bhutan                23) Korea (South)         40) Singapore
 7) Brunei                24) Kuwait                41) Sri Lanka
 8) Cambodia              25) Kyrgyzstan            42) Syria
 9) China                 26) Laos                  43) Taiwan
10) Cyprus                27) Lebanon               44) Tajikistan
11) East Timor            28) Macau                 45) Thailand
12) Georgia               29) Malaysia              46) Turkmenistan
13) Hong Kong             30) Mongolia              47) United Arab Emirates
14) India                 31) Myanmar (Burma)       48) Uzbekistan
15) Indonesia             32) Nepal                 49) Vietnam
16) Iran                  33) Oman                  50) Yemen
17) Iraq                  34) Pakistan
#? 9
Please select one of the following time zone regions.
1) Beijing Time
2) Xinjiang Time
#? 1

The following information has been given:

        China
        Beijing Time

Therefore TZ='Asia/Shanghai' will be used.
Local time is now:      Mon Dec 10 17:46:38 CST 2018.
Universal Time is now:  Mon Dec 10 09:46:38 UTC 2018.
Is the above information OK?
1) Yes
2) No
#? 1

You can make this change permanent for yourself by appending the line
        TZ='Asia/Shanghai'; export TZ
to the file '.profile' in your home directory; then log out and log in again.

Here is that TZ value again, this time on standard output so that you
can use the /usr/bin/tzselect command in shell scripts:
Asia/Shanghai
```

#### `.profile`修改
1. 查看当前时区（当前是英国伦敦时间, 时区是UTC±0）
```
~ $ date -R
Mon, 10 Dec 2018 09:56:19 +0000
```
2. 把`TZ='Asia/Shanghai'; export TZ` 加到`~/.profile`文件中， 如果有其他的TZ配置需要注释掉， 最后输入命令`source ~/.profile`使文件立即生效

3. 确认修改时区是正确的， 北京是UTC+8时区
```
~ $ date -R
Mon, 10 Dec 2018 18:00:20 +0800
```