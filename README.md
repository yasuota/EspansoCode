# My Espanso code

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

</details>

### POP Search
<img src="doc/pop_search.gif" width="900">

After copying the target varnishlog that will be headers to the backend, typing `:varnishlogto` automatically outputs it in the format of a curl command.
This is executed by varnishlogto.py in the scripts folder.

<details>

```
  - trigger: ":pop"
    replace: "{{output}}"
    label: "POP: ADL | City: Adelaide | Country: Australia"
    vars:
      - name: output
        type: shell
        params:
          cmd: 'echo "https://www.google.com/maps/search/?api=1&query=-34.9285,138.6007" | pbcopy'

  - trigger: ":pop"
    replace: "{{output}}"
    label: "POP: AMS | City: Amsterdam | Country: Netherlands"
    vars:
      - name: output
        type: shell
        params:
          cmd: 'echo "https://www.google.com/maps/search/?api=1&query=52.308613,4.763889" | pbcopy'
```


</details>


### POP Search (Metro)
<img src="doc/POP_search_metro.gif" width="900">

<details>

```
  - trigger: ":pop"
    label: "POP: FRA | City: Frankfurt | Country: Germany"
    replace: "{{output}}"
    vars:
    - name: "form1"
      type: form
      params:
        layout: "Metro : EDDF823, ETOU822: [[sample]]"
        fields:
          sample:
            type: choice
            values:
              - TAP SUBMIT
    - name: output
      type: shell
      params:
       cmd: 'echo "https://www.google.com/maps/search/?api=1&query=50.026421,8.543125" | pbcopy'
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
