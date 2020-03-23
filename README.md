# parent-project

Dummy project to test multi module maven project and travis

### Deploy new version
1. Update all submodules to latest
```bash
git submodule update --remote
git add -A
git commit -m "Updated submodules"
git push
```  

2. Create and push tag (triggers deployment to maven repository)

```bash
git tag -a 1.0.3 -m '1.0.3'
git push origin --tags
```

3. Create new SNAPSHOT version

```bash
mvn versions:set -DnewVersion=1.0.4-SNAPSHOT
mvn versions:commit
```

4. Commit and push changes related to version upgrade

```bash
git submodule foreach 'git add pom.xml'
git submodule foreach "git commit -m 'Update version to 1.0.4-SNAPSHOT'"
git submodule foreach 'git push'
git add pom.xml 
git commit -m "Update version to 1.0.4-SNAPSHOT"
git push
```