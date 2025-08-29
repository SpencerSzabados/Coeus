---
title: Physics-coupled spatio-temporal active learning for dynamical systems
authors: Yu Huang, Yufei Tang, Xingquan Zhu, Hanqi Zhuang, Laurent Cherubin
year: 2022
---

# Overview 
The authors investigate the problem of creating a physics informed [[Overview of machine learning|machine learning]] model capable, meaning the model parameters are informed in-part using physical simulation (a method called active learning), of performing spatio-temporal forecasting. The particular problem used throughout the paper is ocean current prediction (forecasting).

The problem of Spatio-temporal forecasting is important within a large variety of scientific domains that deal with dynamic systems (e.,g [[Linear dynamical systems]]) such as earth science, transport planning (such as continuous public transport route optimization), weather forecasting. All the aforementioned examples rely on accurate predictions of spatio-temporal structured data, in the sense that the predicted data reflects real-world phenomena.

With the advent of deep learning and data acquisition sources (e.g., satellite imagery in the case of weather forecasting), machine learning methods are now being applied to spatio-temporal problems. However, even with many new avenues for data acquisition the source of appropriate data for training supervised learning systems remains limited, as any data must be properly ladled and formatted before used, in highly specialized domains. This is one of the central challenges with applying ML based methods for many spatio-temporal forecasting problems.

