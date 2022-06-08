**试翻译页面 https://www.apifox.cn/help/app/mock/**

**（第一小节基本用直译方式，之后我试着把句子改短成比较简洁的意译，感觉这样翻译更加贴切)**
）**

## Mock Feature Explained

Front-end development often relies on back-end API. It is usually difficult to work on the front-end before the back-end API is ready. The Mock feature is designed to solve this exact issue. With the Mock tool, the front-end and back-end can enter the same development phase simultaneously. The front-end can develop and debug the fake data before the back-end interface is ready.

## 1- Feature Summary

The Mock function can automatically generate mock data according to the `API/data definition`, `Mocking rules configurations`, and `Mock Assertion configuration`. A flexible data structure can be generated to meet any user requirements.

By default, Apifox is already capable of generating a set of very user-friendly mock data with `zero configuration`:

1. Based on the data structure and data type from the given API, Apifox can automatically generate all the mocking rules.

2. Apifox has a built-in smart mock function, which intelligently optimises the automatically generated mocking rules according to the field names and data type. For example:


    > A string field that contains `image`, mock generates an image link with URL;
    > 
    > A string field that contains `time`, mock generates a time string;
    > 
    > A string field that contains `city`, mock generates a city name;
    > 

3. Based on built-in rules (which can be turned off), Apifox can identify string fields such as `image`, `avatar`, `username`, `mobile`, `phone`, `url`, `date`, `time`, `timestamp`, `email`, `state`, `city`, `address`, `IP` and more, deriving amazingly realistic mock data.

4. Rules can be customised to override the built-in configurations. Regular expressions and wildcards are supported.

    Mock data output with zero configuration:

```json
{
	"username": "黎勇",
    "phone": "13247278136",
    "age": 23,
    "avatar": "http://dummyimage.com/100x100",
    "description": "广高六被严",
    "location": {
        "province": "江西省",
        "city": "丽江市",
        "address": "安徽省日喀则地区石狮市"
    },
    "registerTime": 72567224950,
    "createAt": "1998-07-24 04:05:01",
    "registerIp": "83.18.192.180"
}
```


**Local mock vs Cloud mock:**

Apifox desktop app runs locally on your computer, and the web version runs on our cloud server.

## 2 - Mock URL Requests

Two types of Mock URLs are supported:

1. API path mode: `http://127.0.0.1:4523/mock/{projectID}/{apiPath}`

2. API ID mode: http://127.0.0.1:4523/mock2/{projectID}/{apiID}`

where request `method` and API defined `method` has to be the same.

For example, if your project ID is `18600`, the required mock API ID is `89343`, the path is `/store/pets`, and the request `method` is `POST`. Then your Mock URL looks like this:

```javascript
// Local Mock URL
POST http://127.0.0.1:4523/m1/18600-0-0/users/123
//OR
POST http://127.0.0.1:4523/m2/18600-0-0/89343

// Cloud Mock URL
POST https://mock.apifox.cn/m1/18600-0-0/users/123
//OR
POST https://mock.apifox.cn/m2/18600-0-0/89343
```

By default, after the `API/data structure` is defined, no extra configuration is required. Mock data can be requested by accessing the URL(s) above.

> **NOTE**
> 1. Local Mock service is hosted at your loopback address `127.0.0.1`. If local network access is required, just change `127.0.0.1` to your computer's local IP address. Check firewall restriction on port `4523` if the mock service is blocked.
> 2. Within the same project, if multiple API connections have the same `method + path`, use **API  ID mode**, and do not use `API path mode` to avoid any request conflict.
> 3. If the API path does not start with `/`, only `API ID mode` will work, not the `API path mode`.
> 4. Mock service starts with the Apifox app by default, no extra action is required.
> 5. Mock service `prefix URL` is fixed and cannot be changed. Changing the `prefix URL in ` `Mock Server` environment settings will not change the actual mock service `prefix URL`.

Obtaining **Mock URL** APIs
Open `API Details` - `View` tab, under `Mock` module. The corresponding mocking URLs are listed here.

(图略)

## 3 - Custom Mocking Rules

Apifox supports very flexible mocking rules to fulfil your requirements.

1.	Data structure defined Mocking Rules

    Manually defined mocking rules are allowed when defining data structure. [Mock.js](https://mockjs.com) is supported. For `Placeholder` style and mocking rules. See [Mock.js syntax](https://mockjs.com/examples.html#DPD) for more information.

    (图略)

2.	Data Field Advanced Settings

    `Max value`, `Min value`, `Array Value`, `Pattern`, `Format` in the Data field `Advanced Settings` will also be used as part of the mocking rules:

    (图略)

3.	Advanced Mock

    Advanced mock is the most flexible way of mocking. The custom data structure can be implemented without any API data structure restrictions. Furthermore, different mock results can be returned based on different request parameters. See [Advanced Mock User Manual]( https://www.apifox.cn/help/app/mock/mock-custom-scripts/) for more information.

4.	Smart Mock

    When the data field(s) in the response (or data model) from the designated API has not been assigned a mocking rule, the system will attempt to use Smart Mock rules to generate the required data to achieve zero configuration at run time and instantly generate user-friendly mock data. See [Smart Mock Manual]( https://www.apifox.cn/help/app/mock/mock-custom-scripts/) for more information.

## 4 - Mock Priority Rules

When data fields are automatically being mocked, the configurations are applied in the following order of priority:

1.	`Assertion` in API Details `Advanced Mock` settings (depends on API parameters matching).

2.	Data field `Mock` rules from data structure configuration.
3.	`Max value`, `Min value`, `Array Value`, `Pattern`, `Format` from Data field `Advanced Settings`.

4.	`Custom Rules` from `Project Settings` - `Smart Mock Settings`.

5.	`In-built Rules` from `Project Settings` - `Smart Mock Settings`.

6.	`Data Type` from Data structure.

## 5 - Miscellaneous

1.	By default, the system will use the first defined `Response` data structure from the mock API. Mock URL(s) for other `Response(s)` can be found in `API Details` - `View` tab under the `Mock` module. 
