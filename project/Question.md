## 用户



### 登录

用户名密码数据验证以及是否匹配，如果成功则生成登录凭证，并返回给前端

login_ticket

user



### 退出

从数据库中更新用户登录凭证

login_ticket



### 注册

对用户提交的信息进行格式校验，判断用户是否存在，对用户密码进行加密,

添加到数据库中发送邮件





请求处理之前从cookie中获取ticket,如果没有则从数据库中获取，判断ticket是否有效-状态，过期时间，并存储在threadLocal中，请求处理之后清空ThreadLocal

## 关注



### 用户关注

存储在redis中的zset中，另外对redis采用事务,实体类型-实体ID，

查询关注列表

```java
Transaction tx = jedisAdapter.multi(jedis);
tx.zadd(followerKey,date.getTime(),String.valueOf(userId));
tx.zadd(followeeKey,date.getTime(),String.valueOf(entityId));
List<Object> resList = jedisAdapter.exec(tx, jedis);
```

### 用户取消关注

在redis删除即可，查询关注列表



### 问题关注取消关注是类似的



### 关注列表

关注列表，个数，当前用户，

查询当前用户的关注状态和取消状态

followed

### 粉丝列表

和关注列表类似



## 消息

### 发送消息

判断用户是否登录，没有登录提示其去登录，否则根据用户要发送的用户名去查找用户，判断该用户是否存在，如果用户存在则添加到数据库中。，并使用消息队列发送消息



### 查询该用户的所有消息

更具用户的ID，去查询它的消息



### 查询消息详情

根据一条消息的会话ID,去查询具体的某一条消息



## 问题

### 提交问题

判断用户是否登录->登录则将问题数据添加到数据库中，并会对问题标题和问题内容进行转义和敏感词过滤

### 问题显示

根据问题ID去查询问题，问题对应的评论，评论的喜欢数量，查询问题的关注者



```java
List<Comment> commentList ===> List<ViewObject>
```



```
EntityType.ENTITY_QUESTION
```

问题的评论

评论的回复









## 评论

### 添加评论

判断用户是否登录，没有登录则跳转到登录界面，否则添加到数据库中，问题的评论数加一，给提问问题的人发送一条消息，xxx评论了你的问题。







## 点赞

### 点赞

判断用户是否登录，在redis中的set进行存储，并统计喜欢的个数，返回喜欢的个数



取消点赞

判断用户是否登录，在redis中的set删除，并统计喜欢的个数，返回喜欢的个数







## 消息队列



### 事件模型

事件类型、触发者、实体类型、实体ID、通知者ID、扩展字段





### 事件类型

登录、注册、评论







### 事件处理器接口

处理事件

支持的事件类型

```java
public interface EventHandler {

    void doHandler(EventModel eventModel);

    /**
      * @author matt
     * @date 2021/1/13
     * @param
     * @return java.util.List<com.matt.project.question.async.EventType>
    */
    List<EventType> listSupportEventType();

}
```

### 事件处理器

事件的处理器去处理事件



### 生产者(触发事件)

生产者：发送事件-》事件模型

list:key 和 事件模型的json串



### 消费者

实现 InitializingBean, ApplicationContextAware，用于获得容器，在执行afterPropertiesSet, 获得容器中所有已经获得的 bean而且是事件处理器类型的对象Map<String, EventHandler> , 遍历事件处理器，遍历这个事件处理器的事件类型，将该事件添加到对应类型的事件中去



```java
private Map<EventType, List<EventHandler>> config = new HashMap<>();
```

启动一个线程去处理事件，从redis中获取消息，查找该事件的事件类型，map中找该事件对应的事件处理器，去处理。







## 表

用户 登录凭证 消息 问题 评论





## 难点

手写消息队列

过滤

redis事务

关注模块-实体类型实体ID





**Caused by: com.mysql.jdbc.exceptions.jdbc4.CommunicationsException: Communications link failure**

由于数据库回收了连接，而系统的缓冲池不知道，继续使用被回收的连接所致的。

mysql默认空闲时间是8H

方法一：修改空闲时间

方法二：可以通过配置，让缓冲池去测试连接是否被回收，如果被回收，则不继续使用







字典树：

end

子树：HashMap<Character, TrieNode>

根据key获取子节点

添加子节点

设置是否是最后一个子节点



实现InitializingBean接口容器启动的时候读取静态文件，将敏感词添加到字典树中去





start, position

遍历字符串，得到一个字符，根据字符去查找子节点，如果子节点空则移动start指针，当前字符安全，如果子节点是字典树的叶子节点则替换，并移动指针

危险

p = p + 1;

start = p

安全

p = p + 1

start = p



否则：

p++







```java
@Service
public class SensitiveServiceImpl implements InitializingBean, SensitiveService {

    /**
     * 默认敏感词替换符
     */
    private static final String DEFAULT_REPLACEMENT = "***";

    @Override
    public void afterPropertiesSet() throws Exception {

        try {
            ClassLoader contextClassLoader = Thread.currentThread().getContextClassLoader();
            InputStream in = contextClassLoader.getResourceAsStream("SensitiveWords.txt");
            InputStreamReader read = new InputStreamReader(in);
            BufferedReader bufferedReader = new BufferedReader(read);
            String word;
            while ((word = bufferedReader.readLine()) != null) {
                word = word.trim();
                addWord(word);
            }
            bufferedReader.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    private class TrieNode {

        private Boolean end = false;

        private Map<Character, TrieNode> subNodes = new HashMap<Character, TrieNode>();

        public void addSubNode(Character key, TrieNode node) {
            subNodes.put(key, node);
        }

        public TrieNode getSubNode(Character key) {
            return subNodes.get(key);
        }

        public Boolean isKeyWordEnd() {
            return this.end;
        }

        public void setKeyWordEnd(Boolean end) {
            this.end = end;
        }
    }

    private TrieNode root = new TrieNode();

    public void addWord(String word) {
        TrieNode tempNode = root;

        for (int i = 0; i < word.length(); i++) {
            Character ch = word.charAt(i);
            if (isSymbol(ch)) {
                continue;
            }

            TrieNode node = tempNode.getSubNode(ch);
            if (node == null) {
                node = new TrieNode();
                tempNode.addSubNode(ch, node);
            }
            tempNode = node;
            if (i == word.length() - 1) {
                tempNode.setKeyWordEnd(true);
            }
        }
    }

    /**
     * 判断是否是一个符号
     */
    private boolean isSymbol(char c) {
        int ic = (int) c;
        // 0x2E80-0x9FFF 东亚文字范围
        return !CharUtils.isAsciiAlphanumeric(c) && (ic < 0x2E80 || ic > 0x9FFF);
    }

    public String filter(String word) {

        if (StringUtils.isBlank(word)) {
            return word;
        }

        StringBuilder result = new StringBuilder();
        String replacement = DEFAULT_REPLACEMENT;
        TrieNode tempNode = root;
        Integer start = 0;
        Integer position = 0;

        while (position < word.length()) {

            Character ch = word.charAt(position);

            // 非法字符
            if (isSymbol(ch)) {
                if (tempNode == root) {
                    result.append(ch);
                    ++start;
                }
                ++position;
                continue;
            }
            tempNode = tempNode.getSubNode(ch);
            if (tempNode == null) {
                result.append(word.charAt(start));
                position = start + 1;
                start = position;
                tempNode = root;
            } else if (tempNode.isKeyWordEnd()) {
                result.append(replacement);
                position = position + 1;
                start = position;
                tempNode = root;
            } else {
                position++;
            }
        }
        result.append(word.substring(start));

        return result.toString();
    }

   /* public static void main(String[] args) throws Exception {
        SensitiveServiceImpl s = new SensitiveServiceImpl();
        //s.afterPropertiesSet();
        s.addWord("色情");
        System.out.println(s.filter("eee色  情"));
    }*/
}

```



**：**通过此次项目，了解了缓存和异步化，以及如何解决缓存和数据库数据的不一致，如何保证消息发送和数据库操作的事务性。