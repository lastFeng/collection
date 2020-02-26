### Redis常用代码

#### RedisTemplate配置

```Java
	@Resource
	private LettuceConnectionFactory lettuceConnectionFactory;

	/**
	* RedisTemplate配置
	**/
	@Bean
	public RedisTemplate<String, Object> redisTemplate(LettuceConnectionFactory lettuceConnectionFactory) {
		// 设置KV映射序列化
		Jackson2JsonRedisSerializer<Object> jackson2JsonRedisSerializer = new Jackson2JsonRedisSerializer<>(Object.class);
		ObjectMapper om = new ObjectMapper();
		
		// 设置可视化
		om.setVisibility(PropertyAccess.ALL, Visibility.ANY);
		om.enableDefaultTyping(DefaultTyping.NON_FINAL);
		jackson2JsonRedisSerializer.setObjectMapper(om);
		
		RedisTempalte<String, Object> template = new RedisTempalte<>();
		redisTemplate.setConnectionFactory(lettuceConnectionFactory);
		// 设置相应的Key与Value的存储序列化
		RedisSerializer<?> stringSerializer = new StringRedisSerializer();
		redisTemplate.setKeySerializer(stringSerializer);
		redisTemplate.setValueSerializer(stringSerializer);
		redisTemplate.setHashKeySerializer(stringSerializer);
		redisTemplate.setHashValueSerializer(stringSerializer);
		
		redisTemplate.afterPropertiesSet();
		
		return redisTemplate;
	}
```