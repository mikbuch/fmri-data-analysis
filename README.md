# General linear model for fMRI data analysis

## Run jupter notebook

```
pipenv run jupyter notebook
```

## Next steps

 1. Provide an exact description of the example data.
 2. Determine which trial form the complete run is the `single trial` that was extracted
 3. Describe how FSL analysis was performed.
 
## How-to initialize git LFS

LFS - large file storage

```bash
git init
git lfs install
```

There are two ways of adding files to git-LFS.

### The first (recommended) method

Create `.gitattributes` file:

```
vim .gitattributes
```

and add the following lines:

```
data/**/* filter=lfs diff=lfs merge=lfs -text
supplementary_materials/**/* filter=lfs diff=lfs merge=lfs -text
```

### The second (not recommended) method

Use the following commands to add directory and all files in this directory and its subdirectories:

```
git lfs track data/**/*
git lfs track supplementary_materials/**/*
```

Note! The command `git lfs track supplementary_materials/**` will not be sufficient to add all files in all subdirectories.

Why this method is **not** recommended: it will add **all** tracked files to your `.gitattributes`, e.g.:

```
➜  fMRI GLM git:(main) ✗ cat .gitattributes

data/res4d.nii.gz filter=lfs diff=lfs merge=lfs -text
data/single_trial filter=lfs diff=lfs merge=lfs -text
data/single_trial/PlanTool_0.txt filter=lfs diff=lfs merge=lfs -text
...
supplementary_materials/feat/example_contrast_plan.feat/rendered_thresh_zstat1.png filter=lfs diff=lfs merge=lfs -text
supplementary_materials/feat/example_contrast_plan.feat/tsplot/ps_tsplot_zstat1_ev1.png filter=lfs diff=lfs merge=lfs -text
supplementary_materials/NIfTI/anatomical filter=lfs diff=lfs merge=lfs -text
supplementary_materials/feat/example_contrast_plan.feat/design.png filter=lfs diff=lfs merge=lfs -text
supplementary_materials/feat/example_contrast_plan.feat/logs/feat2_pre filter=lfs diff=lfs merge=lfs -text
...
```

What you would like to have in your `.gitattributes` is just:

```
data/**/* filter=lfs diff=lfs merge=lfs -text
supplementary_materials/**/* filter=lfs diff=lfs merge=lfs -text
```

See the first (recommended) method.

### Preview the `.gitattributes` file:

```
cat .gitattributes
```

### Add all files to your repository:
```
git add --all
```

### Show which files are tracked with (`git lfs ls-files`)

```
git lfs ls-files
```

**Note!** `git lfs ls-files` works only after you have added the files to the repository with `git add`

Show which files were added to the repository (regardless of whether LFS or not):

```
git status
```

Make sure that the files are tracked with git-LFS:

```
du -sh .git
du -sh .git/lfs
```

If you are using GitHub: make sure that you are using the proper SSH file:
```
cat ~/.ssh/config
```

In GitHub, also make sure that your key is added to you profile (not just one repository!). See the output of a command:

```
ssh -T -ai ~/.ssh/mbuch.pem git@github.com
```

Source: https://superuser.com/a/232406/950943

If you used this key for one repository only you will see somethink like this:

```
Hi mikbuch/your-repository! You've successfully authenticated, but GitHub does not provide shell access.
```

You should see output like this:

```
Hi mikbuch! You've successfully authenticated, but GitHub does not provide shell access.
```

### Pushing to the server

Finally, you can push your reporitory to the remote server:

```
git push -u origin main
```

---

In order to reset:
```
rm -rf .git
rm .gitattributes
```