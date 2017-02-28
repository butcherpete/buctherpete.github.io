---
title: Swift3 
tags: [ios, swift]
keywords:  
last_updated: February 17, 2017
summary: Changes in Swift 3. 
sidebar: notes_sidebar
permalink: ios_swift3.html
folder: notes 
---
[What's new in Swift 3.0](https://www.hackingwithswift.com/swift3)

## Function Labels

"Swift 3 makes all labels required unless you specify otherwise, which means the method names no longer detail their parameters. In practice, this often means the last part of the method name gets moved to be the name of the first parameter."

### Several Basic Types have dropped NS
"In that last call, notice how NSTimer is now just called Timer. Several other basic types have also dropped the "NS" prefix, so you'll now see UserDefaults, FileManager, Data, Date, URL URLRequest, UUID, NotificationCenter, and more."

## Omit needless words

## enums and properites
"UpperCamelCase has been replaced with lowerCamelCase for enums and properties"

## Importing of C functions

## Verbs and Nouns

<blockquote>
Here's are some quotes from the Swift API guidelines:

"When the operation is naturally described by a verb, use the verb’s imperative for the mutating method and apply the “ed” or “ing” suffix to name its nonmutating counterpart"
"Prefer to name the nonmutating variant using the verb’s past participle"
"When adding “ed” is not grammatical because the verb has a direct object, name the nonmutating variant using the verb’s present participle"
"When the operation is naturally described by a noun, use the noun for the nonmutating method and apply the “form” prefix to name its mutating counterpart"
</blockquote>
