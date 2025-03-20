# LightRAG 开发计划

## 1. 前端界面设计
- 设计现代化的用户界面
- 实现响应式布局，支持多设备访问
- 优化用户交互体验
- 添加必要的用户反馈机制
- 实现知识库管理界面
- 添加文档上传和管理功能
- 优化查询和检索界面

## 2. 删除功能优化
- 实现文档级别的删除功能
- 添加批量删除功能
- 实现删除前的确认机制
- 添加删除操作的撤销功能
- 优化删除后的索引更新机制
- 添加删除操作的日志记录

## 3. 知识库分仓管理
- 设计知识库分类系统
- 实现多知识库管理功能
- 添加知识库权限控制
- 实现知识库之间的数据隔离
- 添加知识库导入导出功能
- 实现知识库数据备份和恢复机制

## 4. 响应性能优化
- 优化文档索引性能
- 实现查询结果缓存机制
- 优化向量检索算法
- 实现异步处理机制
- 添加性能监控指标
- 优化数据库查询性能
- 实现分布式部署支持

## 5. 项目代码结构规范
- 重构现有代码结构
- 实现模块化设计
- 添加完整的代码注释
- 规范化命名约定
- 添加单元测试
- 实现持续集成/持续部署
- 完善项目文档

## 6. vLLM 部署方式
- 集成 vLLM 推理引擎
- 实现模型量化支持
- 优化推理性能
- 添加模型版本管理
- 实现模型热更新
- 添加模型监控指标
- 优化资源利用

## 7. 主流大模型 API 集成
- 集成 OpenAI GPT API
- 集成 Google Gemini API
- 集成 Anthropic Claude API
- 实现统一的 API 调用接口
- 添加 API 密钥管理
- 实现 API 调用限流
- 添加错误处理和重试机制
- 实现模型切换功能

## 时间规划
建议按照以下顺序进行开发：
1. 项目代码结构规范（基础工作）
2. 前端界面设计（提升用户体验）
3. 删除功能优化（完善基础功能）
4. 知识库分仓管理（扩展功能）
5. 响应性能优化（提升系统质量）
6. vLLM 部署方式（优化推理性能）
7. 主流大模型 API 集成（扩展模型支持）

## 注意事项
- 每个功能点都需要进行充分的测试
- 保持代码质量和文档更新
- 注意系统安全性
- 考虑向后兼容性
- 保持性能监控
- 定期进行代码审查 


## 执行


知识库分仓：
1.添加参数：k_db_name
初始化阶段使用默认知识库、默认知识库不不可删除

修改处：
（1）文件的加载、增删（添加k_db_name参数）参数：working-dir（知识库文件夹）、input-dir（知识库源文件文件夹）
（2）知识库的增加、删除（以k_db_name为参数）
（3）关闭启动后本地文件上传
（4）文件删除后本地文件同步删除（重写函数：clear_documents）

3.20
已经实施：
document_routers:
    scan_directory_for_new_files:添加参数：k_db_name:str = "default_k_db",
    run_scanning_process:添加参数（内部调用：scan_directory_for_new_files）：k_db_name:str
    upload_to_input_dir(上传文件函数):添加参数:k_db_name添加分仓上传功能
    insert_file(上传文件函数):添加参数:k_db_name
    insert_batch(批量上传文件函数):添加参数:k_db_name
以完成文件上传通过参数：k_db_name上传至不同地文件路径，默认路径：default_k_db
修改LightRAG类：添加output参数控制知识库分类
    query，aquery添加参数kn_name:用于控制检索知识库
    类添加参数：current_kb: str = field(default="default_kn_name")默认知识库
    apipeline_enqueue_documents添加参数kb_name 
    函数ainsert_custom_kg、aquery_with_separate_keyword_extraction、adelete_by_doc_id



