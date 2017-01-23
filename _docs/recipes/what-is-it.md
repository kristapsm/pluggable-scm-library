---
layout: docs
title: What is Pluggable SCM Library
permalink: /docs/recipes/what-is-it/
---

# Documentation

## `public interface SCMProvider`

This interfaces defines the specification of an SCMProvider.

## `public Closure get(String projectName, String repoName, String branchName, String credentialId, Closure extras)`

Return a closure representation of SCM section.

 * **Parameters:**
   * `projectName` — - name of the project.
   * `repoName` — - name of the repository to checkout.
   * `branchName` — - name of the branch to checkout.
   * `credentialId` — - name of the credential in the Jenkins credential

     manager to use.
   * `extras` — - extra closures to add to the SCM section.
 * **Returns:** a closure representation of the SCM providers SCM section.

     <p>

## `public Closure trigger(String projectName, String repoName, String branchName)`

Return a closure representation of the SCM providers trigger SCM section.

 * **Parameters:**
   * `projectName` — - name of the project.
   * `repoName` — - name of the repository to checkout.
   * `branchName` — - name of the branch checkout on ref updates.
 * **Returns:** closure representation of the SCM providers trigger SCM section.

## `public void createScmRepos(String workspace, String repoNamespace, String codeReviewEnabled, String overwriteRepos) }`

Creates the relevant repositories defined by your cartridge in your chosen SCM provider

 * **Parameters:**
   * `workspace` — Workspace of the cartridge loader job
   * `namespace` — Location in your SCM provider where your repositories will be created
   * `overwriteRepos` — Whether the contents of your created repositories are over-written or not

     <p>