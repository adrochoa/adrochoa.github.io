---
title: "Excel Formulae"
date: 2022-08-06T19:27:00-07:00
draft: false
---

Here I will keep a list of useful formulae in Microsoft Excel.
These will probably also work in other spreadsheet software.

## Lookup all values with corresponding key (spill)

    =FILTER($$key_range,key=$$value_range)

## Lookup right to left

    =INDEX($$total_range,MATCH(key,$$key_range,FALSE),1)

## Two way lookup

    =INDEX($$value_only_range,MATCH(row_key,$$row_range,FALSE),MATCH(column_key,$$column_range,FALSE))

## Get every *n*th column (negative *n* goes backward)

    =OFFSET($first_cell,0,n*(COLUMN()-COLUMN($first_lookup_cell)))

## Get every *n*th row (negative *n* goes backward)

    =OFFSET($first_cell,n*(ROW()-ROW($first_lookup_cell)),0)