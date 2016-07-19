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







