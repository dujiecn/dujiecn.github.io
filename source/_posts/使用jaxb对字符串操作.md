---
title: 使用jaxb对字符串操作
date: 2016-09-19 11:11:33
tags: ["JAXB"]
---

### 对象转xml字符串

	/**
	 * 
	 * @param obj
	 * @XmlAccessorType(XmlAccessType.FIELD) @XmlRootElement(name = "xml")
	 * @param encoding
	 * @return
	 */
	public static String convertToXml(Object obj, String encoding) {
		String result = null;
		try {
			JAXBContext context = JAXBContext.newInstance(obj.getClass());
			Marshaller marshaller = context.createMarshaller();
			marshaller.setProperty(Marshaller.JAXB_FORMATTED_OUTPUT, true);
			marshaller.setProperty(Marshaller.JAXB_ENCODING, encoding);

			StringWriter writer = new StringWriter();
			marshaller.marshal(obj, writer);
			result = writer.toString();
		} catch (Exception e) {
			e.printStackTrace();
		}

		return result;
	}
	
### xml字符串转java对象

	public static <T> T converToJavaBean(String xml, Class<T> clazz) {
		try {
			JAXBContext context = JAXBContext.newInstance(clazz);
			Unmarshaller unmarshaller = context.createUnmarshaller();
			AbstractUnmarshallerImpl abstractUnmarshallerImpl = (AbstractUnmarshallerImpl) unmarshaller;
			return (T) abstractUnmarshallerImpl.unmarshal(new StringReader(xml));
		} catch (Exception e) {
			throw new RuntimeException(e);
		}
	}	

可能出现的错误：SAXNotRecognizedException: Feature 'http://javax.xml.XMLConstants/feature/secure-

本地模式运行是好的，服务器模式下运行报错。原因是本地的jdk运行环境是1.7，服务器运行环境是1.8。所以导致此异常。
开发环境里面可以设置eclipse的jre