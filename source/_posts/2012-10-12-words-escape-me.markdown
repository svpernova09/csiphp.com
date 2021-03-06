---
author: jeremykendall
comments: true
date: 2012-10-12 08:00:30
layout: post
slug: words-escape-me
title: Words escape me
wordpress_id: 637
categories:
- PHP
---

Look, I know this is going to be tough to read, and I usually try to post short, snappy code snippets, but this is just too good.  Or sad.  Whatever.  Words truly escape me.

Take it away anonymous submitter: 

> "Look at all these standalone ternaries for validating form input. What a mess! They're embedded in what would normally be controller logic.  These should be if() statements or, preferably, a separate validating class."

Indeed.

``` php
<?php

(!is_numeric($input['raw_gpa']) || $input['raw_gpa'] < 0 || $input['raw_gpa'] > 4) ? ($errors[] = "Your unweighted GPA must be between 0 and 4. You must indicate your unweighted GPA, and this must be between 0 and 4.") : ('');
($input['gpa_max'] < 0 || $input['gpa_max'] > 200) ? ($errors[] = "Your school's max possible GPA must be between 0 and 100.") : ('');
($input['gpa'] < 0 || $input['gpa'] > $input['gpa_max']) ? ($errors[] = "Your weighted GPA must be between 0 and your school's max weighted GPA.") : ('');

(($input['act'] == "") && (($input['sat_verb'] == "") || ($input['sat_math'] == ""))) ? ($errors[] = "To use this site, you must indicate your SAT scores, or your ACT scores, or both.") : ('');

(!is_numeric($input['act']) && ($input['act'] != "")) ? ($errors[] = "Your ACT score must be a numeric value, or blank.") : ('');
(!is_numeric($input['act_eng']) && (!empty($input['act_eng']))) ? ($errors[] = "Your ACT English score must be a numeric value, or blank.") : ('');
(!is_numeric($input['act_math']) && (!empty($input['act_math']))) ? ($errors[] = "Your ACT Math score must be a numeric value, or blank.") : ('');
(!is_numeric($input['act_read']) && (!empty($input['act_read']))) ? ($errors[] = "Your ACT Reading score must be a numeric value, or blank.") : ('');
(!is_numeric($input['act_sci']) && (!empty($input['act_sci']))) ? ($errors[] = "Your ACT Science score must be a numeric value, or blank.") : ('');

(!is_numeric($input['sat_math']) && ($input['sat_math'] != "")) ? ($errors[] = "Your SAT math must be a numeric value, or blank.") : ('');
(!is_numeric($input['sat_verb']) && ($input['sat_verb'] != "")) ? ($errors[] = "Your SAT verbal must be a numeric value, or blank.") : ('');
(!is_numeric($input['sat_writ']) && ($input['sat_writ'] != "")) ? ($errors[] = "Your SAT writing must be a numeric value, or blank.") : ('');

((($input['act'] > 36) || ($input['act'] < 1)) && ($input['act'] != "")) ? ($errors[] = "Your ACT score is out of the valid range.") : ('');
((($input['act_eng'] > 36) || ($input['act_eng'] < 1)) && ($input['act_eng'] != "")) ? ($errors[] = "Your ACT English score is out of the valid range.") : ('');
((($input['act_math'] > 36) || ($input['act_math'] < 1)) && ($input['act_math'] != "")) ? ($errors[] = "Your ACT Math score is out of the valid range.") : ('');
((($input['act_read'] > 36) || ($input['act_read'] < 1)) && ($input['act_read'] != "")) ? ($errors[] = "Your ACT Reading score is out of the valid range.") : ('');
((($input['act_sci'] > 36) || ($input['act_sci'] < 1)) && ($input['act_sci'] != "")) ? ($errors[] = "Your ACT Science score is out of the valid range.") : ('');
((($input['sat_math'] > 800) || ($input['sat_math'] < 200)) && ($input['sat_math'] != "")) ? ($errors[] = "Your SAT math score is out of the valid range.") : ('');
((($input['sat_verb'] > 800) || ($input['sat_verb'] < 200)) && ($input['sat_verb'] != "")) ? ($errors[] = "Your SAT verbal score is out of the valid range.") : ('');
((($input['sat_writ'] > 800) || ($input['sat_writ'] < 200)) && ($input['sat_writ'] != "")) ? ($errors[] = "Your SAT writing score is out of the valid range.") : ('');

((($input['psat'] > 240) || ($input['psat'] < 60)) && ($input['psat'] != "")) ? ($errors[] = "Your PSAT is out of the valid range.") : ('');

(!array_key_exists($input['nat_merit'], $nationalMeritArray)) ? ($errors[] = "Please indicate whether or not you were awarded National Merit or National Achievement awards.") : ('');
(!array_key_exists($input['ap'], $apCountArray)) ? ($errors[] = "Please estimate how many APs your school offers.") : ('');

(!array_key_exists($input['hs_type'], $hs_type_array)) ? ($errors[] = "Please indicate what type of high school you attend (public, private, magnet, etc.).") : ('');
(!array_key_exists($input['hs_state'], $state_array)) ? ($errors[] = "Please indicate the state that your high school is in.") : ('');
($input['hs_city'] == "") ? ($errors[] = "Please indicate the city that your high school is in.") : ('');

(array_search($input['decile'], $decile_array) === false) ? ($errors[] = "Please indicate your class rank.") : ('');

((!is_numeric($input['class_size']) || $input['class_size'] < 1 || $input['class_size'] > 10000) && $input['class_size'] != "") ? ($errors[] = "If you indicate your class size, it must be numeric (without words, periods, or commas).") : ('');
```
