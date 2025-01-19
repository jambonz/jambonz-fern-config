# jambonz Developer Documentation
This repository contains the configuration for the jambonz Developer Docs. The outlined structure can be used as an outline to inspire your own documentation. 

Click [here](https://jambonz-12u348932.docs.buildwithfern.com) to see the generated website. 

## How to update documentation?
First, make sure you've downloaded the Fern CLI
```
npm install -g fern-api
```

To view your changes live in a locally-hosted environment, run
```
fern docs dev
```

To update your documentation, run
```
fern generate --docs
```

To preview your documentation, run
```
fern generate --docs --preview
```

The repository contains GitHub workflows that automatically runs these commands for you. For example, when you make a PR a preview link auto-generates and when you merge to main the docs site updates.