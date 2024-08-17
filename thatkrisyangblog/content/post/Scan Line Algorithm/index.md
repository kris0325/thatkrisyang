---
title: Scan Line Algorithm
description: 掃瞄線算法
slug: Scan Line Algorithm
date: 2024-08-16
image: 1.png
categories:
    - leetcode
tags:
    - Scan Line Algorithm
    
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---
# 什麼是掃描線
以“391.同時在天上的飛機最大數量”問題為例

思路1:暴力掃描
遍歷每一時刻，檢測每個時刻有多少飛機

思路2:掃描線
不需要檢測每一時刻，只需檢測起點或終點的位置的時刻！（交點變化的位置，只有起點或者終點（才會影響天上飛機的數量））

# 算法模板

```java
//interval question template : 391.Count Of AirLanes 數天上飛機
//一般有兩種解法
//1.使用priority queue 
//2.或者將start/end分開進行掃描線處理
//考點：sort 的comparator寫法，判斷interval merge的邊界條件
/*
 * 391.Count Of AirLanes
 */
public class Solution{
    //scan line 扫描线 算法 question
    //lintcode question description： 391.天上同时出现飞机的最多数量
    //给出飞机的起飞与降落时间的列表，用序列interval表示，请计算出天上最多有多少架飞机？
    //注意：多家爱飞机降落与起飞在同一时刻，我们任务降落有优先权

    //思路：
    //1事件点：我们将飞机的起飞时间视为一个“进入”事件，降落时间视为一个“离开”事件。然后，我们将这些事件按照时间排序处理。
    //2事件排序：按照时间先后对所有事件排序。如果时间相同，“离开”事件优先于“进入”事件，因为飞机降落时不会再占用天空。
    //3扫描线处理：我们从前向后扫描这些事件，并维护一个当前飞机数量的计数器。在每个“进入”事件时计数器加1，在每个“离开”事件时计数器减1，同时更新最大飞机数量。
    public int countOfAirLanes(List<Interval> airplanes) {
        int maxCount = 0;
        int currentCount = 0;
        List<Event> allEvents = new ArrayList<>();
        for (Interval interval : airplanes) {
            //起飞事件
            allEvents.add(new Event(interval.start, true));
            //降落事件
            allEvents.add(new Event(interval.end, false));
        }
        //对事件按时间胜序排序：时间相同的情况，降落事件优先
        Collections.sort(allEvents,(a,b) -> {
            if (a.time == b.time) {
                return a.isStart ? 1 : -1;
            }
            return a.time - b.time;
        });

        for (Event event : allEvents) {
            //起飞，currentCount加1
            if (event.isStart) {
                currentCount++;
            } else {
                //降落，currentCount加-1
                currentCount--;
            }
            //更新最大飞机数量
            maxCount = Math.max(maxCount, currentCount);
        }
        return maxCount;
    }

    class Event {
        //飞机起飞/降落时间
        int time;
        //飞机是否是起飞事件
        boolean isStart;
        public Event(int time, boolean isStart) {
            this.time = time;
            this.isStart = isStart;
        }
    }
    class Interval {
        //飞机起飞时间
        int start = 0;
        //飞机降落时间
        int end = 0;
    }
}
```

# leetcode題單
```
391.Count Of AirLanes
56.Merge Intervals
57.Insert Intervals
1272.removeInterval
435.NonOverlappingIntervals
1288.RemoveCoveredIntervals
352.DataStreamAsDisjointIntervals
1229.MeetingScheduler
986.IntervalListIntersections
759.employeeFreeTime
218.TheSkylineProblem
```

