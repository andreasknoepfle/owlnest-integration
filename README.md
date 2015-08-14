# Gitlab CI with Extraction Framework Validation
- Install Owlnest https://github.com/andreasknoepfle/docker-owlnest
- Install Gitlab-CI with the same version as Owlnest Gitlab (currently 7.9 branch)
- Install Gitlab-Runner
- Install Maven and Checkout the extraction frameworkl

- Add Gitlab Application with return url: http://[gitlab-ci-url]/user_sessions/callback
- Open up Gitlab CI and configure it with App ID and App Secret from Gitlab (last step)
- Add the projecte with the ontology and the mappings to Gitlab CI
- Start a Runner with the Token from Gitlab CI
- Add The Following Job (adjust the path in the first line):

```
EXTRACTION_FRAMEWORK_PATH=/path/to/the/framework

git submodule update --init
ONTOLOGY=$(readlink -f ontology.owl)
MAPPINGS=$(readlink -f mappings)
cd EXTRACTION_FRAMEWORK_PATH
mvn exec:java -Dexec.mainClass="org.dbpedia.extraction.dump.validate.ValidateMappings" -Dexec.args="$ONTOLOGY $MAPPINGS" 
```
