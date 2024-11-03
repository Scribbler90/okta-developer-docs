---
title: Basic sign-in flow with the password factor
---

<ApiLifecycle access="ie" />

This guide explains how to enable a password-only sign-in flow in your web app using the embedded SDK.

> **Note**: Passwords are a security vulnerability because they can be easily stolen and can leave a system prone to phishing attacks. Provide your users with the ability to use other authenticators by replacing password-only sign-in experiences with either a [password-optional](https://developer.okta.com/docs/guides/pwd-optional-overview) or a multifactor experience.
<StackSnippet snippet="pwdoptionalusecase" />

---

#### Learning outcomes

- Add a password-only sign-in flow to a server-side web app.

#### What you need

<StackSnippet snippet="whatyouneed" />
<br />

#### Sample code

<StackSnippet snippet="samplecode" />

---

## Configuration updates

To configure your app so it requires only a password, see <StackSnippet snippet="configureyourapp" inline />.

## Summary of steps

<StackSnippet snippet="summaryofsteps" />

## Integration steps

<StackSnippet snippet="integrationsteps" />

<StackSnippet snippet="getuserprofile" />
