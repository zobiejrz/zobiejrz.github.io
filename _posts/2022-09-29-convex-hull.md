---
title: Convex Hull
date: 2022-09-29 13:00:00 -0400
categories: [School Projects, Algorithm Design & Analysis]
tags: [Python, Divide & Conquer]
pin: false
math: false
mermaid: true
image:
  path: /assets/lib/2022-09-29-convex-hull/convex-hull.png
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  alt: Sample Convex Hull
---

## Introduction

A convex hull of a set of points is the smallest convex polygon for which each point in the set is either on the boundary or in its interior. In this project I had the opportunity to develop a divide and conquer algorithm for this problem.

## Algorithm

The divide and conquer algorithm for this project is based on this principle: If I have two convex hulls of a set of points, I can find two tangent lines that will combine the two convex hulls into one.

To do this I define a convex hull to be an array of points on the edge of the hull. Points on the interior are not represented. I construct the arrays such that each adjacent index in the arrays are adjacent points in the convex hull, which means I don't need to waste any time complexity resorting the array (after one initial sort). Starting with the two points in each hull closest to each other, I look at the slope of the line between the two points. I then find the four points (two for the 'top' tangent and two for the 'bottom' tangent) that will combine the two hulls. I then remove all the points that are now considered interior nodes and finalize the new convex hull.

To initialize this algorithm I first sort the points by x-coordinate, left to right. I then split the resulting array in half until a base case of single points, which then combine up to be the convex hull of the whole set.

## Complexity

The time complexity of this algorithm ended up being $O(nlogn)$, and the space complexity was $O(n^2logn)$.

## Summary

Learning about divide and conquer algorithms was really interesting. I think its so cool how the master theorem describes the time complexity of all divide and conquer algorithms in relation to the time complexity of a single iteration. I also gained lots of practical experience by developing this convex hull solver.
