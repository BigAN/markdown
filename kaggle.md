# kaggle

## 特征工程

"site_id", "site_domain", "app_id", "banner_pos", "device_id_count", "device_conn_type", "C16", "device_ip_count", "device_id_site_id_count", "device_ip_site_id_count", "device_model".





\- hour, device_ip and C17 were removed from my feature set, because they did not help.
\- quadratic interactions between major features and all others.
  The features which had greater impacts on my score were 
                 device_model, app_id, site_id, site_domain and banner_pos.
\- cubic interactions among major features.
\- three types of count features (inspired by additions by Yannick Martel for tinrtgu code.    Thanks Martel and tinrtgu):

1. 1. 1. 1. 1. 1. device_ip, device_id, device_ip * device_id and so on counted in all datasets.
      2. the same features counted in past 24 hours.
      3. the same features counted in reverse event order in 24 hours ahead.

- click rate for each feature with Laplace smoothing.



doc_id 点击率，  



