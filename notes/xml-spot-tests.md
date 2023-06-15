# Spot checks on existing xml raw files

Propublica: 215ms
https://pp-990-xml.s3.us-east-1.amazonaws.com/202211369349309441_public.xml?response-content-disposition=inline&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA266MJEJYTM5WAG5Y%2F20230615%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20230615T140409Z&X-Amz-Expires=1800&X-Amz-SignedHeaders=host&X-Amz-Signature=6cf9b7f4bc1541d61e9e471ddf5048a63d401034e4978a77b4f42774518dc1d0


[ACCESS DENIED]:
https://pp-990-xml.s3.us-east-1.amazonaws.com/202211369349309441_public.xml


[ACCESS GRANTED]: 119ms
https://opendata.grantseeker.io/data/202211369349309441_public.xml


API TEST
EIN = "481249429" (CVE / KAUFFMAN FELLOWS)

https://projects.propublica.org/nonprofits/api/v2/organizations/481249429.json

>>> most recent data == FY Ending 2020-06-30 as of 2023-06-15
(https://projects.propublica.org/nonprofits/download-filing?path=04_2021_prefixes_47-51%2F481249429_202006_990_2021041317935530.pdf)

...vs. most recent available xml data for 2021-06-30 [IE SUBSEQUENT YEAR]:
https://opendata.grantseeker.io/data/202211369349309441_public.xml




