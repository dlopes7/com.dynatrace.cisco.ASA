# Instruction for creating an extension from scratch

> Please start from **0. Begin** and follow sections in order, step by step

## 0. Begin

1. **new repository name** should be `com.dynatrace.<device-family>.<device>`
1. [create a new repo from this template](https://github.com/dynatrace-extensions/template-snmp/generate)
1. clone the newly created repository
>example name: `com.dynatrace.palo-alto.PA-5260` (hint: for wider range use `generic` in place of the `<device>`)
## x. Hacks for now
> You'll see `direnv: error /$something/$something/$repo/.envrc is blocked. Run 'direnv allow' to approve its content`. We kindly advise to you ignore it and carry on. If you se it then everything is going well.
1. run the following commands
```
repo="<newly-created-repo-name>"
# fill the blank in above

git clone git@github.com:dynatrace-extensions/palo-alto.generic.git
cp palo-alto.generic/default.nix $repo
cp palo-alto.generic/go-datasource.nix $repo
cp palo-alto.generic/go-deps.nix $repo
cp palo-alto.generic/Makefile $repo
cp -r palo-alto.generic/scripts/ $repo
cp palo-alto.generic/local-activation.json $repo
cp palo-alto.generic/remote-activation.json $repo
rm -rf palo-alto.generic
cd $repo
rm -f todo
```
2. ignore lines starting with "..." in this instruction

## 1. Prerequisite verification

> This step **might** take a considerable amount of time, bandwith and CPU, especially if nix is foreign to you. All of this will happen almost instantly upon most of subseqent plugin creation attempts

1. make sure all the [prerequsistes from README](https://github.com/dynatrace-extensions/template-snmp#prerequisites) are satisfied if you haven't done that already
2. `make init`
1. for the first time this may take a few minutes, depending on your network conection, don't be discouraged
1. then it may take a minute or so while furiously spitting out vast amount of text to the console, reamin brave!
1. run `make prerequisites-verify`, exit code should be 0, *might* display encouragement message as well
 
## 2. Initial setup

- edit the `README.md` and fill the blanks (hint: `<something>` is a blank)
- edit `src/extension.yaml` and fill the blanks (hint: `extension-fqn` is the repo name)
- ... <- somehow run the extension without companion to verify it's correct?

## 3. Companion setup
- you'll need `.snmprec` data, consider checking [this repo](https://github.com/etingof/snmpsim-data) or EF1 resources if your extension is a port
- put the data in `companion/snmp-data`, the inside directories can be nested arbitrarily (but this will need to be reflected in activation configs in the auth section)
- metric variation can be configured via [this guide](https://snmplabs.thola.io/snmpsim/documentation/simulation-with-variation-modules.html#variate-numeric), it's particularly usefull for animating charts
- edit `local-activation.json` - `[0].value.snmp.devices.[0].authentication.community` should reflect the filestructure in `companion/snmp-data` without the `.snmprec` suffix, so for following:
```
[λ] ~/Desktop/palo-alto-extension-ef-2/companion/snmp-data (main) >_ tree
.
└── network
    └── firewall
        └── paloalto-pa-5000.snmprec

2 directories, 1 file
```
the value would be: `"network/firewall/paloalto-pa-5000"`
- `make run`
- there should be a metric outputed with the key you've inserted in previos steps

## 4. Tenant integration
- set up `remote-activation.json`, you'll also need an snmpsim running where a AGs assigned to the tenant can reach it; this step is vague on purpose, if you don't understand how to do it reffer to wiki / ask someone
- `make all`
- input required secrets, the instructions on how to do it will be provided
- enjoy your extension being uploaded to the tenant

## 5. Demo
...

## Post

- remember to add featuresets to local acitvation configuration when adding more metrics!
- feel free to delete this instruction
