# My Espanso code

## Basic command 

<img src="doc/linux.gif" width="900">

<details>

First, copy a valid IP address, then type :ip to display its information. And it is copied to your clipboard.

<summary>Sample Code</summary>

```
  - trigger: ":ip"
    replace: "{{output}}"
    label: "ip"
    vars:
      - name: output
        type: shell
        params:
          cmd: '/usr/bin/curl "ipinfo.io/$(pbpaste)" && whois -h bgp.tools $(pbpaste)'
      - name: clipboard_contents
        type: clipboard

```
</details>

</details>


## Type a dynamic variable

<img src="doc/curl.gif" width="900">

<details>

When you type :curl, options to select either Performance option or Normal appears. After selecting one, you can enter the domain to access. The curl command is displayed directly at the cursor. 

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

You can easily check Fastly's POP name, country, and area by typing `:pop` anywhere. 
And its geolocation data is copied to your clipboard, so you can check the location on Google Maps.
https://www.fastly.com/documentation/guides/concepts/pop/

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
