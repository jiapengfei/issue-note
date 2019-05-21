# Java

## Error: Could not find or load main class Test.class
    命令行中，Java执行class文件不要加.class后缀，注意包名；-cp或者-classpath指定依赖路径

[JVM 类加载机制详解](http://www.importnew.com/25295.html)

[java虚拟机：运行时常量池](https://www.cnblogs.com/xiaotian15/p/6971353.html)

[java--遇到NoSuchMethodError通用解决思路](https://www.cnblogs.com/xiaoMzjm/p/4566672.html)

[关于java.ext.dirs——使用路径启动main class](https://blog.csdn.net/scugxl/article/details/43240991)

[Java指令-Djava.ext.dirs的陷阱——加上jre默认路径](https://blog.csdn.net/cyony/article/details/74375251)

## HttpClient绕过https协议，设置server username password

```Java
private String getOAuth2Token() throws IOException {
    String token = null;
    CloseableHttpClient client = null;
    try {
        SSLContext sslcontext = createIgnoreVerifySSL();
        Registry<ConnectionSocketFactory> socketFactoryRegistry = RegistryBuilder.<ConnectionSocketFactory>create()
                .register("http", PlainConnectionSocketFactory.INSTANCE)
                .register("https", new SSLConnectionSocketFactory(sslcontext)).build();
        PoolingHttpClientConnectionManager connManager = new PoolingHttpClientConnectionManager(
                socketFactoryRegistry);
        HttpClients.custom().setConnectionManager(connManager);

        CredentialsProvider credentialsProvider = new BasicCredentialsProvider();
        credentialsProvider.setCredentials(AuthScope.ANY,
                new UsernamePasswordCredentials("username", "password"));

        client = HttpClients.custom().setConnectionManager(connManager)
                .setDefaultCredentialsProvider(credentialsProvider).build();
        HttpPost httpPost = new HttpPost("https://xxx");
        List<NameValuePair> nvps = new ArrayList<NameValuePair>();
        nvps.add(new BasicNameValuePair("data_name", "data_value"));
        httpPost.setEntity(new UrlEncodedFormEntity(nvps, "utf-8"));

        CloseableHttpResponse response = client.execute(httpPost);

        HttpEntity responseEntity = response.getEntity();
        if (responseEntity != null) {
            String responseBody = EntityUtils.toString(responseEntity, "UTF-8");
            JSONObject jsonObject = new JSONObject(responseBody);
            token = (String) jsonObject.get("access_token");
        }
        EntityUtils.consume(responseEntity);
        response.close();
        System.out.println("token: " + token);
    } catch (Exception e) {
        log.error("get OAuth2 Token from server failed", e);
    } finally {
        if (client != null) {
            client.close();
        }
    }
    return token;
}

private SSLContext createIgnoreVerifySSL() throws NoSuchAlgorithmException, KeyManagementException {
    SSLContext sc = SSLContext.getInstance("SSLv3");
    X509TrustManager trustManager = new X509TrustManager() {
        @Override
        public void checkClientTrusted(java.security.cert.X509Certificate[] paramArrayOfX509Certificate,
                String paramString) throws CertificateException {
        }

        @Override
        public void checkServerTrusted(java.security.cert.X509Certificate[] paramArrayOfX509Certificate,
                String paramString) throws CertificateException {
        }

        @Override
        public java.security.cert.X509Certificate[] getAcceptedIssuers() {
            return null;
        }
    };
    sc.init(null, new TrustManager[] { trustManager }, null);
    return sc;
}
```
