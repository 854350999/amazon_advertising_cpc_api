## The basic package of Amazon advertising api call

## 1、Get authorization

In the first step, you need to get authorized uri based on your developer information

```python
import adapi
auth_api = adapi.Auth(client_id=client_id,
                      client_secret=client_secret,
                      redirect_uri=redirect_uri,
                      region="NA")
auth_uri = auth_api.get_grant_url()
```

Click on this url and log in with your own store, and you will see a code on the URL information, this code is what we need

## 2、Get access_token and refresh_token

In the second step, you need to obtain **refresh_token** and **access_token** according to the **code** obtained in the previous step

```python
access_token, refresh_token = auth_api.get_refresh_token(code=code)
```

Get **access_token** and **refresh_token** through this method, save this **refresh_token** in your own notepad for permanent use

**access_token** has a validity period, if you want to get a new **access_token**, you can directly

```python
access_token = auth_api.get_new_access_token(refresh_token=refresh_token)
```

## 3、Get profiles

In the third step, you need to obtain the **profile_id** of your store according to the **access_token** obtained in the previous step

```python
profile_api = adapi.Profiles(access_token=access_token, 
                             region=region, 
                             client_id=client_id)
response = profile_api.get_profiles()
```

## 4、For example
if you want use report api
```python
report_api = adapi.sp_products.Reports(access_token=access_token,
                                       profile_id=profile_id,
                                       region=region,
                                       client_id=client_id)
response = report_api.create_report(record_type=record_type,
                                    params=params)
```
