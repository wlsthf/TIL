# java ) Masking 처리

```java
/**
	 * 이름을 마스킹 처리 한다.
	 * 홍*동, 남**민, 홍*
	 * jame*****, t**
	 * @param name
	 * @return
	 */
	public static String maskName(String name) {
		
		// 한글
		if(	name.matches(".*[ㄱ-ㅎㅏ-ㅣ가-힣]+.*")) {
			char[] ch = name.toCharArray();
			
			for ( int i = 0 ; i < ch.length ; i ++ ) {
				
				// 3글자 이상일 경우 처리 (앞,뒤 한글자만 보이고 마스킹
				if ( ch.length > 2 ) {
					if ( i != 0 && i != ch.length-1 ) ch[i] = '*';
					
				// 2글자인 경우
				} else {
					if ( i != 0 ) ch[i] = '*';
				}
			}
			
			return String.valueOf(ch);
			
		// 영문
		} else {
			char[] ch = name.toCharArray();
			
			for ( int i = 0 ; i < ch.length ; i ++ ) {
				
				// 4자리 이상일 경우
				if ( ch.length > 4 ) {
					if ( i > 3 ) ch[i] = '*';
					
				// 2글자인 경우
				} else {
					if ( i > 0 ) ch[i] = '*';
				}
			}
			
			return String.valueOf(ch);
		}
	}
	
	
	
	/**
	 * 전화번호 마스킹처리 (010-1**-**78, 010-12**-**78)
	 * @param num
	 * @return
	 */
	public static String maskPhone(String num) {
		
		if ( num.length() < 13 ) return "";
		
		String[] tmp = num.split("-");
		char[] ch = tmp[1].toCharArray();
		
		for ( int i = 0 ; i < ch.length ; i++ ) {
			if ( i == ch.length-1 || i == ch.length-2 ) ch[i] = '*';
		}
		
		char[] ch2 = tmp[2].toCharArray();
		
		for ( int j = 0 ; j < ch2.length ; j++ ) {
			if ( j < 2 ) ch2[j] = '*';
		}
		
		return tmp[0] + "-" + String.valueOf(ch) + "-" + String.valueOf(ch2);
	}
	
	
	
	/**
	 * 이메일 마스킹처리 (영문이름 마스킹과 통일하고 도메일은 그대로 노출)
	 * @param email
	 * @return
	 */
	public static String maskEmail(String email) {
	
		if ( email.indexOf("@") > -1 ) {
			String[] tmp = email.split("@");
			char[] ch = tmp[0].toCharArray();
			
			for ( int i = 0 ; i < ch.length ; i++ ) {
				
				// 4자리 이상일 경우
				if ( ch.length > 4 ) {
					if ( i > 3 ) ch[i] = '*';
					
				// 2글자인 경우
				} else {
					if ( i > 0 ) ch[i] = '*';
				}
			}
			return String.valueOf(ch) + "@" + tmp[1];
		} else {
			return "";
		}
	}
	
```

