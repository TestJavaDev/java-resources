---
layout: default
title: Home
nav_order: 1
description: "Java Resources"
permalink: /
---

<button class="btn js-toggle-dark-mode">Preview dark color scheme</button>

<script>
const toggleDarkMode = document.querySelector('.js-toggle-dark-mode');

jtd.addEvent(toggleDarkMode, 'click', function(){
  if (jtd.getTheme() === 'dark') {
    jtd.setTheme('light');
    toggleDarkMode.textContent = 'Preview dark color scheme';
  } else {
    jtd.setTheme('dark');
    toggleDarkMode.textContent = 'Return to the light side';
  }
});
</script>

#  Interview preparation resources

- [Coding Interview University](https://github.com/jwasham/coding-interview-university#why-use-it)

- <a href="https://leetcode.com/explore/">LeetCode</a>
- <a href="https://www.interviewbit.com/practice/">InterviewBit</a>
- <a href="https://www.hackerrank.com/">HackerRank</a>

