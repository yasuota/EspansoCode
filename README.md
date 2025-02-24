# espanso

## Sample

<img src="doc/curl.gif" width="900">

<details>

<summary>Sample Code</summary>

```
matches:
  - trigger: ":curl"
    replace: "curl -svo /dev/nul -w 'http_code:%{http_code}\\ntime_namelookup:%{time_namelookup}\\ntime_connect:%{time_connect}\\ntime_appconnect:%{time_appconnect}\\ntime_pretransfer:%{time_pretransfer}\\ntime_starttransfer:%{time_starttransfer}\\ntime_total:%{time_total}\\n' https://{{form1.name}}"
    label: "curl performance"
    vars:
    - name: form1
      type: form
      params:
        layout: |
          Type in Domain [[name]]

  - trigger: ":curl"
    replace: "curl -svo /dev/nul -w 'http_code:%{http_code}\\ntime_namelookup:%{time_namelookup}\\ntime_connect:%{time_connect}\\ntime_appconnect:%{time_appconnect}\\ntime_pretransfer:%{time_pretransfer}\\ntime_starttransfer:%{time_starttransfer}\\ntime_total:%{time_total}\\n' https://{{form1.name}} --resolve '{{form1.name}}:443:{{form1.ip}}'"
    label: "curl performance with resolve"
    vars:
    - name: form1
      type: form
      params:
        layout: "Type in Domain [[name]] \nType in IP [[ip]]"
```
</details>


### Setup 

1. Install using Homebrew
See below for details.
https://espanso.org/docs/install/mac/

2. Git clone
```
git clone https://github.com/fastly/espanso-conf.git
```

3. Copy this github Config to your folder

```
cp -R ./espanso-conf/espanso/match/* $HOME/Library/Application\ Support/espanso/match/
```
See below for details.
https://espanso.org/docs/configuration/basics/#structure 
