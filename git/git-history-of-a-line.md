# Git history of a line

Sometimes I want to see the history of the changes to a line over time.

Today, I needed to see when we released a new version of the [Azure Functions package](https://github.com/elastic/integrations/tree/main/packages/azure_functions) at https://github.com/elastic/integrations/blob/3f2be218f3c458ce40670b19a1ec722113e0cd08/packages/azure_functions/manifest.yml#L4.

```shell
$ git log -L '/version: 0.1.1/,+1:manifest.yml'
commit a15b2755deac186743e4de887f276f135a226102
Author: devamanv <aman.verma@elastic.co>
Date:   Tue Jul 25 02:27:12 2023 +0530

    Initial commit to add a datastream for Azure Functions metrics

diff --git a/packages/azure_functions/manifest.yml b/packages/azure_functions/manifest.yml
--- a/packages/azure_functions/manifest.yml
+++ b/packages/azure_functions/manifest.yml
@@ -4,1 +4,1 @@
-version: 0.0.1
+version: 0.1.1

commit 2d586eb8b988385231575ba6bc151687287003e8
Author: Aman Verma <38116245+devamanv@users.noreply.github.com>
Date:   Wed Jul 19 14:44:12 2023 +0530

    Add Logs data stream for collecting Azure Functions (#6417)

diff --git a/packages/azure_functions/manifest.yml b/packages/azure_functions/manifest.yml
--- /dev/null
+++ b/packages/azure_functions/manifest.yml
@@ -0,0 +4,1 @@
+version: 0.0.1
```

Refs: https://stackoverflow.com/questions/50469927/view-git-history-of-specific-line
