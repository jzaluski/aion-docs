This section will take you through installation of the [Aion solo mining pool](doc:solo-mining-pool), which should be used with the [external miner](doc:external-miner). During the initial Kilimanjaro (Aion Phase 1) launch, only the Aion solo miner was officially supported on the network. We have since released Aion pool mining software for individuals to run their own pools:
[block:callout]
{
  "type": "info",
  "title": "Aion Pool 2",
  "body": "- [Blog Post](https://blog.aion.network/new-aion-pool-software-6e3232527fa) (overview and features)\n- [Github](https://github.com/aionnetwork/aion_pool2) (guide and installation)"
}
[/block]

[block:api-header]
{
  "title": "Solo Pool vs. Public Pool"
}
[/block]
A solo pool has one node mining for rewards at the network difficulty, with the full payout to the one account. With a public pool (not covered in this document), a group of nodes work together, distributing a reward proportional to each node's work when a block is mined by the pool. Often, there are fees associated with joining a public pool, and although rewards are received more consistently in a public pool, this may not guarantee benefit over solo-mining.

You can find a list of public pools that mine Aion under [External Resources](doc:external-resources).

# Solo-mining Pools

[block:api-header]
{
  "title": "Prerequisites"
}
[/block]
In order to run the solo mining pool, you must already have:
- Aion [node](doc:node-set-up) and [external miner](doc:external-miner)
- Python v2.7*

*Included by default with Ubuntu desktop, may need to be installed separately in Ubuntu server (see below):
[block:callout]
{
  "type": "warning",
  "title": "Python installation (if necessary):",
  "body": "1. Open terminal\n2. Run the following commands:\n\n```bash\nsudo apt-get update \nsudo apt-get install build-essential make \nsudo apt-get install python2.7 python-dev\n```"
}
[/block]

[block:api-header]
{
  "title": "Update Configure File"
}
[/block]
You will have to modify the **config.xml** file in the aion directory (aion/config/config.xml) before running the mining pool. Update the following fields in the *consensus* section:
[block:parameters]
{
  "data": {
    "h-0": "Field",
    "h-1": "Configuration",
    "0-0": "**Mining**",
    "1-0": "**Miner-address**",
    "0-1": "Set to false to disable internal mining",
    "1-1": "The wallet address that will collect mined rewards. The account address created in creating accounts section can be used for this purpose"
  },
  "cols": 2,
  "rows": 2
}
[/block]
Example of an updated consensus section to enable external mining:
[block:code]
{
  "codes": [
    {
      "code": "<consensus>\n  <mining>false</mining>\n  <miner-address>0xa0----------------your-account-address--------------------------</miner-address>\n  <cpu-mine-threads>8</cpu-mine-threads>\n  <extra-data>AION</extra-data>\n<consensus>",
      "language": "xml"
    }
  ]
}
[/block]
In the *APIs enabled* section, verify that the "stratum" option is included.
[block:code]
{
  "codes": [
    {
      "code": "<apis-enabled>web3,eth,personal,stratum</apis-enabled>",
      "language": "xml"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Install and Run"
}
[/block]
1. Download the latest prepackaged mining pool file **aion-solo-pool-{version}.tar.gz** from the aion_miner [release page](https://github.com/aionnetwork/aion_miner/releases)
2. Extract the file to the desired directory
3. Open terminal in **aion-solo-pool-{VERSION}** directory, run the command

```
./configure.sh
```
[block:callout]
{
  "type": "warning",
  "title": "Note",
  "body": "The **configure.sh** script may take several minutes to complete, and should only be run once."
}
[/block]
4. Once the script completes, run:

```
./run_quickstart.sh
```
5. Launch the Aion kernel in a **separate terminal** (Navigate to the **aion** directory and run: 

```
./aion.sh
```

**If you now have the kernel, miner, and solo-mining-pool running, congrats! You're now mining on Aion.**
[block:callout]
{
  "type": "info",
  "title": "Check Balance",
  "body": "You can check your balance by inputting your address at the top of the Aion [dashboard](https://mainnet.aion.network/#/dashboard)."
}
[/block]