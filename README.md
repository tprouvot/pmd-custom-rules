# This repo contains PMD rules to extends the defaults ones for Salesforce

Inspired by the video [Custom PMD rules for any Metadata within minutes](https://www.londonscalling.net/sessions/custom-pmd-rules-for-any-metadata-within-minutes/) of Robert Sosemann [related repository](https://github.com/rsoesemann/unhappy-soup/)

## Troubleshooting
I had some troubles when trying to use the PMD Rule designer to build those rules, if you face the issue `You seem to be missing the JavaFX runtime.
Please install JavaFX on your system and try again` [this](https://github.com/pmd/pmd/discussions/4153) helped me to solve it.
## How to use those rules?

### With PMD
`pmd --minimum-priority 2 -d force-app -R ./custom-ruleset.xml -f text -l apex`

### With Salesforce Code Analyzer
[Documentation](https://forcedotcom.github.io/sfdx-scanner/en/v3.x/custom-rules/author/#pmd-custom-rules)

## Rules

### Flow
``` xml
   <rule name="MetadataRequiresDescription" language="xml"
      message="Add a description to explain the Flow"
      class="net.sourceforge.pmd.lang.rule.XPathRule">
      <priority>2</priority>
      <properties>
         <property name="version" value="2.0" />
         <property name="xpath">
            <value><![CDATA[
               //document/Flow[not(description)]
       ]]></value>
         </property>
      </properties>
   </rule>
   <rule name="ExcessiveFlowLength" language="xml" message="Excessive Flow length."
      class="net.sourceforge.pmd.lang.rule.XPathRule">
      <priority>2</priority>
      <properties>
         <property name="version" value="2.0" />
         <property name="xpath">
            <value><![CDATA[
               //document/Flow[pmd:endLine(.) > 2000]
          ]]></value>
         </property>
      </properties>
   </rule>
```
### Custom Fields / Objects
``` xml
    <rule name="MetadataRequiresDescription" language="xml" message="Add a description to explain custom metadata" class="net.sourceforge.pmd.lang.rule.XPathRule">
        <priority>2</priority>
        <properties>
            <property name="version" value="2.0"/>
            <property name="xpath"><value><![CDATA[
                    //(CustomObject | CustomField)[not(description)]
            ]]></value></property>
        </properties>
    </rule>
```

### Global metadata
``` xml
      <rule name="BumpApiVersion" language="xml" message="Metadata should use the latest API version."
      class="net.sourceforge.pmd.lang.rule.XPathRule">
      <priority>1</priority>
      <properties>
         <property name="version" value="2.0" />
         <property name="xpath">
            <value><![CDATA[
               //apiVersion/text[number(@Image) > 46 and number(@Image) < 48]
          ]]></value>
         </property>
      </properties>
   </rule>
```
