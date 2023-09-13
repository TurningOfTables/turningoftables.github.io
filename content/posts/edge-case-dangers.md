---
title: "The dangers of overplaying the edge case card"
date: 2023-02-19T16:38:18Z
draft: false
icon: 🎴
---

Making lots of small decisions that are suboptimal but only affect a small amount of your user base is deceptively damaging over time.<!--more-->

It's commonplace to be faced with the following following choice during development:

a) Do something quick and easy to implement, but which knowingly annoys a tiny proportion of your users.

b) Do something slower and harder to implement, but which makes your users happy.

Generally the resulting decision in my experience has been a), and I can initially understand why. It allows you to keep things moving forward, and it appears to have a very small cost.

However, beware of making these decisions over and over again and seeing them as individual choices rather than cumulative.

Your first decision of a) annoys 0.5% of your users (for example). Who cares! It's an edge case that you can't spend your time worrying about. There are bigger fish to fry.

You then forget about it in the next release, and make another a) decision in a different feature. +0.5% annoyed users.

You then forget about it in the next release, and make another a) decision in a different feature. +0.5% annoyed users.

You then forget about it in the next release, and make another a) decision in a different feature. +0.5% annoyed users.

You then forget about it in the next release, and make another a) decision in a different feature. +0.5% annoyed users.

You then forget about it in the next release, and make another a) decision in a different feature. +0.5% annoyed users.

You then forget about it in the next release, and make another a) decision in a different feature. +0.5% annoyed users.

You then forget about it in the next release, and make another a) decision in a different feature. +0.5% annoyed users.

You then forget about it in the next release, and make another a) decision in a different feature. +0.5% annoyed users.

You then forget about it in the next release, and make another a) decision in a different feature. +0.5% annoyed users.

Now 5% of your users are annoyed. Decisions like this go on and on, without any view of their cumulative effects on the overall project. Of course these numbers are all illustrative - the groups of annoyed users might overlap, and you might be gaining more happy users with your new features than you are annoying with your compromises.

Far be it from me to suggest that compromises aren't sometimes required, and in fact I'm a strong believer in the idea that the perfect (software) is the enemy of the good (software) - but be very keenly aware that while you may be making different decisions on disparate features, they don't disappear in the next release - they accumulate.