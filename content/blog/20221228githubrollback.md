---
title: "Rollback in GitHub Desktop"
date: 2022-12-28
slug: 2022/12/28/github-rollback
summary: Rollback in GitHub Desktop
categories: 
  - Misc
---

## Step 1

Choose **the project** you want to rollback in GitHub Desktop, as presented in Figure 1.

{{<figure src="/contents/blog/20221228-1.png" caption="Figure 1">}}

## Step 2

Click the **History** in Figure 2, find the newest commit, and click right mouse button, and choose **Revert changes in commit**.

{{<figure src="/contents/blog/20221228-2.png" caption="Figure 2">}}

## Step 3

If you completed step 2 successfully, you will see the changes like Figure 3 **green box**. These mean the project creates a new "commit" record rather than being restored immediately.

Click the **Changes**.

{{<figure src="/contents/blog/20221228-3.png" caption="Figure 3">}}

## Step4

Click the **Push origin**. Then you will get your original project before the committed.

{{<figure src="/contents/blog/20221228-4.png" caption="Figure 4">}}

## Reference

- [Rollback uncommitted changes in GitHub Desktop (or Github for Windows)](https://stackoverflow.com/questions/24975043/rollback-uncommitted-changes-in-github-desktop-or-github-for-windows)

- [GitHub Desktop rollback](https://jiming.blog.csdn.net/article/details/112615134?spm=1001.2101.3001.6650.17&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-17-112615134-blog-80140863.pc_relevant_3mothn_strategy_recovery&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-17-112615134-blog-80140863.pc_relevant_3mothn_strategy_recovery&utm_relevant_index=23)