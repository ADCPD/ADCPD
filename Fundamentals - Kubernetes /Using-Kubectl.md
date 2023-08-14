# Kubernetes : Fundamentals
---

## Current context

Get the current context:

```bash
  kubectl config current-context
```

## List all contexts


List all the contexts:

```bash
  kubectl config get-contexts
```

## Change context

Use a context:

```bash
  kubectl config use-context [contextName]
```

## Using kubectx

What's great about Kubernetes is the incredible amount of tools created by the community and available for free.  Kubectx is a simple tool that provides an easy way to list and change context.

You can install it on:

Windows (if you have Chocolatey installed):

```bash
    choco install kubectx-ps
```

macOS (if you have Brew installed):

```bash
    brew install kubectx
```

Ubuntu:

```bash
    sudo apt install kubectx
```

To list the contexts, simply type:

```bash
    kubectx
```

To change context:

```bash
    kubectx <contextName>
```

## Rename context

Rename context:

```bash
  kubectl config rename-context [old-name] [new-name]
```

## Delete context

Delete context:
```bash
    kubectl config delete-context [contextName]
```
