# General linear model for fMRI data analysis

Part of the materials from this repository is described in the publication by the author -- [Functional Magnetic Resonance Imaging Signal Modelling and Contrasts: an Example of Manual Praxis Tasks](https://cmst.eu/articles/functional-magnetic-resonance-imaging-signal-modelling-and-contrasts-an-example-of-manual-praxis-tasks/) (Buchwald, 2021). In particular the Jupyter Notebook called [Functional magnetic resonance imaging signal modelling and contrasts](https://github.com/mikbuch/fmri-data-analysis/blob/main/Functional%20magnetic%20resonance%20imaging%20signal%20modelling%20and%20contrasts%20on%20the%20example%20of%20manual%20praxis%20tasks.ipynb) was used to calculate model parameters and visualize the results.

Most of the data used in the examples in this repository come from a study by [Przybylski & Króliczaj, 2017; JINS, Cambridge University Press](https://www.cambridge.org/core/journals/journal-of-the-international-neuropsychological-society/article/planning-functional-grasps-of-simple-tools-invokes-the-handindependent-praxis-representation-network-an-fmri-study/FA52E09E77D85F016BFBF04379CB8CAC).


| ![image](https://user-images.githubusercontent.com/10733514/147957866-1558557b-5ae4-4b74-a93a-c07da219c80d.png) |
|---|
| Figure 1 from [Buchwald, 2021](https://cmst.eu/articles/functional-magnetic-resonance-imaging-signal-modelling-and-contrasts-an-example-of-manual-praxis-tasks/)|.

## Run jupter notebook

```
pipenv run jupyter notebook
```

## TODO

 1. Provide an exact description of the example data.
 2. Determine which trial form the complete run is the `single trial` that was extracted
 3. Describe how FSL analysis was performed.
 
## How-to initialize git LFS

LFS - large file storage

Make sure that you have `git lfs` installed (how-to install for: [macOS](https://docs.github.com/en/repositories/working-with-files/managing-large-files/installing-git-large-file-storage), [Linux](https://github.com/git-lfs/git-lfs/wiki/Installation#debian-and-ubuntu)). In short: `brew install git-lfs`.

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

In order to reset (if needed/optional) during the process:

```
rm -rf .git
rm .gitattributes
```

---

Additional resources:

 * 045 Introduction to Git LFS (Large File Storage) by Dan Gitschooldude: https://youtu.be/xPFLAAhuGy0
