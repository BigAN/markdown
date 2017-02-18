# 用户model

## feas 说明

```python
phone,none,,True,
day_total_order_num,number#freq#10,,False,
mean_order_mean_jiange,number#freq#5,0#0.2,False,
mean_time_before_submit,number#dis,1000#50000,False,
mean_search_times,number,0#0.5,True,
mean_visit_pois_before_submit,number#dis#7,2#1000,False,
mean_is_use_envelope,number,,True,
mean_preview_times,number,,False,
mean_check_comment_times,number,,True,
mean_comment_times_bf_submit,number,0#0.5,True,
mean_has_check_orders,number,0#0.2,False,
mean_in_poi_with_orderlist,number#freq#5,0#0.3,False,
mean_as_share_envelope,number#dis,,True,
mean_comment_times_af_submit,number#dis#3,0#0.7,True,
mean_time_after_submit,number#dis#5,300#3600,True,
fir_one_poi_rate,number#dis#5,0#0.61,False,
sec_one_poi_rate,number#dis#10,0#0.3,False,
order_behave_rate,number#dis#4,0#0.3,True,
user_suggest_type,cate,0,True,
payed_arrived_rate,number#dis#5,0.5#10,False,
in_scope_rate,none,0.5#10,False,
mean_dis,number#dis,0#0.2,False,
aor_id_num,none,,True,
recipient_address_num,number,0#15,True,
fei_order_num,number#freq#5,0#15,False,
food_continus_days,number#freq#6,0#2,True,
7day14ord_days,number#dis,0#4,True,"一天2单"
outofrange_days,number,0#5,False,"配送不在范围天数"
max_continue_order_num,number,0#4,True,"用户最长连续下单天数(每天1单或2单)"
all_order_ratio,number#freq#5,0#0.8,False,"访购率"
aver_order,number,,False,"周订单量"
start_order_ratio,none,,Flase,"前两周访购率"
start_time_before_120s,none,,Trhe,"下单时间在120s内占比"
all_time_before_120s,none,,True,"所有时间在120s内占比"
act_ord_num,none,,True,"活动单数量"
act_cost_per_ord,number#freq#7,0#1,False,"每单美团成单成本"
punish_poi_num,none,0#3,True,"下单商家中被处罚商家数量"
addr_num,none,,True,"地址数量"
none_high_cnt,none,,True,"非高峰下单（重提，定义高峰）"
max_duration_length,none,,Flase,"","最长连续下单天数（重提）"
dm_num,none,,True,"设备数量"
dm_set,none,,True,"设备集合"
out_range_ord_cnt_act_rate,number,0#0.5,False,"订单不在范围比率"
last_date,none,,Flase,"活动单下单最后日期"
mean_punish_period_ord_rate,number,0#0.9,False,
mean_punish_poi_ord_rate,number,0#0.8,False,
neg_type,cate,0,True,"1。。。"
punish_status,cate,,True,"处罚状态"
```

## dim_user_feature

### 改写部分

```python
recipient_phone 

online_pay_rate  > online_pay_count

in_scope_rate > in_scope_count

mean_dis > above8000_count

recipient_address_num > recipient_address_array

order_num > ord_num

fir_one_poi_rate,sec_one_poi_rate > week:poi_num

behaves_dates,order_dates > week behaves_dates,order_dates

user_suggest_type > week user_suggest_type


fact_ord_submitted_risk
fact_xianfu_waimai_log_access
dim_user_relation__uuid_phone__line
fact_user_categoried

```







### 验证下cases af filter

- neg type的数据对吗？



## feature 说明

```
1.特征名称,2.处理方法(none 不做处理,number#dis#5 等距处理并分割成5份。可以支持等频,cate 类别处理),3.过滤范围(过滤掉不想加入model的部分)，4.是否作为单独特征，5.特征范围。
phone,none,,True,
day_total_order_num,number#freq#5,0#3,True,3.006#3.447#4.167#5.381#8.537#121.162
mean_order_mean_jiange,number#freq#5,0#0.3,False,0.3#0.346#0.4#0.458#0.54#1.0
mean_time_before_submit,number#dis,1000#50000,False,0.0#83.333#166.667#250.0#333.333#416.666#500.0#583.333#666.666#750.0#833.333#916.666#1000.0
mean_search_times,number,0#0.4,True,0.4#0.439#0.48#0.502#0.562#0.623#0.686#0.762#0.857#0.979#1.136#1.503#23.0
mean_visit_pois_before_submit,number,2#1000,False,0.0#0.731#0.857#0.928#1.0#1.059#1.19#1.325#1.45#1.571#1.7#1.835#2.0
mean_is_use_envelope,number,0#0.5,True,0.5#0.538#0.571#0.603#0.639#0.673#0.714#0.75#0.796#0.84#0.889#0.943#1.0
mean_preview_times,number,0#0.3,False,0.3#0.579#0.744#0.857#0.947#1.005#1.093#1.177#1.276#1.406#1.591#1.962#70.818#617.75
mean_check_comment_times,number,,False,0.0
mean_comment_times_bf_submit,number,0#0.5,True,0.504#0.533#0.556#0.583#0.611#0.638#0.667#0.722#0.75#0.833#0.938#1.143#5.684#11.0
mean_has_check_orders,number,0#0.3,False,0.3#0.333#0.364#0.399#0.435#0.479#0.514#0.571#0.632#0.706#0.8#0.9#1.0
mean_in_poi_with_orderlist,number#freq#5,0#0.3,False,0.3#0.333#0.375#0.471#0.524#1.0
mean_as_share_envelope,number#dis,,True,0.0#0.083#0.167#0.25#0.333#0.417#0.5#0.583#0.667#0.75#0.833#0.917#1.0
mean_comment_times_af_submit,number#dis#3,0#0.7,True,0.7#0.8#0.9#1.0
mean_time_after_submit,number#dis#5,300#3600,False,0.0#60.0#119.999#179.999#239.999#299.998
fir_one_poi_rate,number#dis#5,0#0.7,False,0.7#0.76#0.82#0.88#0.94#1.0
sec_one_poi_rate,number#dis#10,0#0.6,False,0.6#0.64#0.68#0.72#0.76#0.8#0.84#0.88#0.92#0.96#1.0
order_behave_rate,number#dis#4,0#0.5,True,0.502#28.126#55.751#83.375#111.0
user_suggest_type,cate,0,False,1#2
payed_arrived_rate,number#dis#5,0.5#10,False,0.0#0.1#0.199#0.299#0.399#0.498
in_scope_rate,none,0.5#10,False,
mean_dis,number#dis,0#0.3,False,0.301#0.359#0.418#0.476#0.534#0.592#0.651#0.709#0.767#0.825#0.884#0.942#1.0
recipient_address_num,number,0#7,True,8.0#9.0#10.0#11.0#12.0#13.0#16.0#21.0#1519.0
all_order_num,number#freq#5,0#15,False,16.0#22.0#31.0#43.0#86.0#7711.0
food_continus_days,number#freq#6,0#2,False,3.0#4.0#5.0#40.0
7day14ord_days,number#dis,0#6,False,7.0#13.667#20.333#27.0#33.667#40.333#47.0#53.667#60.333#67.0#73.667#80.333#87.0
outofrange_days,none,0#5,True,
max_continue_order_num,none,0#10,True,
all_order_ratio,none,0#0.8,True,
aver_order,number,0#3,False,3.017#3.2#3.4#3.667#4.0#4.286#4.667#5.167#5.839#6.6#7.7#9.5#296.577
start_order_ratio,none,,False,
start_time_before_120s,none,,True,
all_time_before_120s,none,,True,
act_ord_num,none,,True,
act_cost_per_ord,number#freq#7,0#1,False,1.0#1.745#2.5#3.36#4.4#5.812#8.156#146.667
punish_poi_num,none,0#3,True,
addr_num,none,,True,
none_high_cnt,none,,True,
max_duration_length,none,,False,
dm_num,none,,True,
dm_set,none,,True,
out_range_ord_cnt_act_rate,number,0#0.5,False,0.502#0.593#0.673#0.75#0.818#0.871#0.917#0.955#1.0#4.773
last_date,none,,False,
mean_punish_period_ord_rate,number,0#0.8,False,0.8#0.855#0.89#0.925#0.952#0.965#0.983#1.0
mean_punish_poi_ord_rate,number,0#0.8,False,0.8#0.96#1.0
neg_type,cate,0,True,1#3
one_day_high,number#freq#5,0#4,True,5.0#6.0#7.0#10.0#17.0#466.0
one_week_high,number#freq#5,0#10,True,11.0#12.0#13.0#17.0#29.0#473.0
dist_food,number#freq#5,0#5,True,6.0#10.0#14.0#20.0#34.0#922.0
food_ratio,number,0#0.3,False,0.3#0.333#0.357#0.4#0.5#0.556#0.8#1.0
food_total,number,,False,1.0#2.0#3.0#4.0#6.0#1118.0
most_food_lianxu_danliang,number#freq,0#5,True,6.0#7.0#8.0#9.0#10.0#12.0#16.0#20.0#33.0#486.0
diff_avg_general_score,none,,True,
comment_rate_ratio,none,,True,
top1_vary_food_delivery_ord_num,none,,True,
top1_add_comment_ord_num,none,,True,
top_comment_rate,none,,True,
label_comment_rate_ratio,none,,True,
text_comment_rate_ratio,none,,True,
ord_num__avg_score__ratio,none,,True,
punish_status,cate,,True,
mean_order_mean_jiange&one_day_high&one_week_high,pair,,True,
one_day_high&one_week_high&food_ratio&most_food_lianxu_danliang,pair,,True,
fir_one_poi_rate&7day14ord_days&food_continus_days&aver_order,pair,,True,
mean_in_poi_with_orderlist&all_order_num&aver_order,pair,,True,
mean_visit_pois_before_submit&day_total_order_num&fir_one_poi_rate&act_cost_per_ord,pair,,True,
mean_punish_poi_ord_rate&mean_punish_period_ord_rate&aver_order,pair,,True,
day_total_order_num&mean_time_before_submit&mean_visit_pois_before_submit&fir_one_poi_rate&mean_has_check_orders,pair,,True,
user_suggest_type&payed_arrived_rate&aver_order,pair,,True,
mean_dis&out_range_ord_cnt_act_rate&sec_one_poi_rate&aver_order,pair,,True,
```

## 周订单小于2分析

13,855,615,796 多次登录

13,975,156,382 距离异常下单

15147101255 多次登录

15255320605 单日单量过高

15280233862 wifimac 一对多

15590888558 支付账号一对多

15,755,025,679 支付账号一对多

15,860,728,117 距离异常下单

17,712,759,551 订单多次支付

18,002,335,343 



| a.name![img](http://stat.sankuai.com/static/images/_.gif?ts=1471258119&dt=20160815&type=xlsfile&creator=105681&filename=__sys_savesql_465ede2b62%2F%E8%91%A3%E5%81%A5_2016_08_15_16_22_54__2016_08_15_18_48_39&xmlid=) | a.co |
| ---------------------------------------- | ---- |
| NULL                                     | 847  |
| 支付账号一对多                                  | 727  |
| 距离异常下单                                   | 561  |
| 订单多次支付                                   | 430  |
| 团伙刷单策略体系                                 | 388  |
| 多次登陆                                     | 312  |
| 模型产出                                     | 246  |
| 用户集中度策略体系                                | 199  |
| 非主流机型                                    | 192  |
| wifimac一对多，只有一个商家                        | 170  |
| 处罚商家再上线                                  | 142  |
| wifiMac下两个商家处罚80％或者46均衡分                 | 130  |
| 单日高频大于20废弃                               | 124  |
| 同一uuid多绑定手机号                             | 105  |
| sim_mobile反查封禁                           | 100  |
| v1商家100单                                 | 89   |
| 处罚商家管理用户                                 | 80   |
| 人工                                       | 76   |
| 单日高频小于20                                 | 42   |
| 下单密集度                                    | 40   |
| 单家众包5单以上                                 | 38   |
| 多次首购资格用户                                 | 34   |
| 每日超高频下单用户                                | 32   |
| geohash一对多，一个商家                          | 31   |
| 运营市场反馈                                   | 30   |
| 异常接单手机号月单量                               | 23   |
| 恶意下单用户                                   | 10   |
| 注册时间反向聚合                                 | 5    |
| token一对多                                 | 4    |

- 支付账号一对多

  ​	可以干掉。

- ​

保留

## 用户集中度

AUC 

相对于acc 区分了

- 在正负样本的准确率
- 在正负样本的召回率
- 只要有一个不好，那么auc的值就会低。

用户feas



## 联合刷单

输入

> phone，poi，单量

中间



## 样本更新

拦截表:

```
origindb.wmrisk02_waimai_risk__message_center_ugc_punish_record
mart_waimai_risk.wm_risk_strategy_hit_record
```