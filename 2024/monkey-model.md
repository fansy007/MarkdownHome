# request
```json
{
   "soeid": "string",  // 开发者的唯一标识符，如姓名或员工编号
   "commits": [
        {
            "commitId": "string",        // 提交的唯一标识符
            "time": "string",            // 提交的时间戳
            "author": "string",          // 提交作者的唯一标识符
            "message": "string",         // 提交说明信息
            "filesChanged": 0,           // 变更的文件数量
            "modifiedFiles": [           // 修改的文件详细信息
                {
                    "name": "string",         // 文件名
                    "type": "string",         // 文件类型（如"code", "config", "doc"等）
                    "lines": {
                        "added": 0,          // 添加的行数
                        "deleted": 0,        // 删除的行数
                        "modified": 0        // 修改的行数
                    },
                    "tags": {                // 文件内容的标识和标签
                        "methodDefine": 0,   // 定义了多少个方法
                        "complexity": 0,     // 代码复杂度（如循环嵌套、条件分支数量等）
                        "refactoring": 0,    // 重构程度
                        "testing": 0         // 测试覆盖率或测试相关的代码行
                    }
                }
            ]
        }
   ],
   "reviewsByOthers": [
        {
            "reviewId": "string",         // 审查的唯一标识符
            "time": "string",             // 审查时间戳
            "reviewer": ["string"],       // 审查你代码的开发者唯一标识符数组
            "reviewedPerson": "string",   // 被审查者的唯一标识符（应为你自己）
            "comments": 0,                // 审查中提供的评论数量
            "feedbackType": "string",     // 审查反馈类型（如"positive", "neutral", "negative"）
            "commitsReviewed": [          // 审查过的提交信息
                {
                    "commitId": "string",   // 关联的提交ID
                    "author": "string"      // 提交者的唯一标识符（应为你自己）
                }
            ],
            "reviewTags": [                // 审查的标签，用于标记审查的性质
                "string"                   // 如"code_quality", "performance", "security"等
            ]
        }
   ],
   "reviewsByYou": [
        {
            "reviewId": "string",         // 代码审查的唯一标识符
            "time": "string",             // 审查时间戳
            "reviewer": ["string"],       // 审查的开发者唯一标识符数组（应为你自己）
            "reviewedPerson": "string",   // 被审查者的唯一标识符
            "comments": 0,                // 审查中提供的评论数量
            "feedbackType": "string",     // 审查反馈类型（如"positive", "neutral", "negative"）
            "commitsReviewed": [          // 审查过的提交信息
                {
                    "commitId": "string",   // 关联的提交ID
                    "author": "string"      // 提交者的唯一标识符
                }
            ],
            "reviewTags": [                // 审查的标签，用于标记审查的性质
                "string"                   // 如"code_quality", "performance", "security"等
            ]
        }
   ],
   "jiraIssues": [
        {
            "issueId": "string",             // JIRA问题的唯一标识符
            "summary": "string",             // JIRA问题的简述
            "description": "string",         // JIRA问题的详细描述
            "pts": 0,                        // 故事点数
            "label": "string",               // JIRA标签（如"bug", "feature", "improvement"等）
            "status": "string",              // JIRA问题的状态（如"open", "in progress", "done"等）
            "priority": "string",            // 问题的优先级（如"low", "medium", "high", "critical"）
            "epic": "string",                // 史诗（Epic）的名称
            "component": ["string"],         // 受影响的组件列表
            "moduleCount": 0,                // 该JIRA问题涉及的模块数量
            "commitsCount": 0,               // 关联的提交数量
            "prCount": 0,                    // 关联的Pull Request数量
            "relatedPrs": ["string"],        // 关联的Pull Request ID列表
            "assignee": "string",            // 分配到的开发者
            "reporter": "string",            // 问题的报告者
            "createdTime": "string",         // 问题创建时间
            "updatedTime": "string",         // 问题最后更新时间
            "resolvedTime": "string",        // 问题解决时间（如果已解决）
            "comments": [                    // JIRA问题下的评论列表
                {
                    "commentId": "string",   // 评论的唯一标识符
                    "author": "string",      // 评论者的唯一标识符
                    "time": "string",        // 评论时间戳
                    "body": "string"         // 评论内容
                }
            ]
        }
    ]
}
```

# response
```json
{
    "soeid": "dev5678",   // 开发者的唯一标识符
    "personalities": [
        {
            "codeType": "full-stack",    // 推断开发者可能具有全栈开发经验。可能选项: "frontend", "backend", "full-stack"
            "commitTimePattern": "afternoon", // 假设开发者在下午进行代码提交。可能选项: "morning", "afternoon", "evening", "night"
            "strength": "tech",    // 开发者的强项为技术。可能选项: "tech", "business", "documentation", "testing"
            "collaborationStyle": "team-player" // 基于他们的工作和代码审查行为推断。可能选项: "independent", "team-player", "review-focused"
        }
    ],
    "advice": [
        {
            "roleFit": "tech lead",     // 适合的角色建议。可能选项: "developer", "tech lead", "team-lead", "project-manager"
            "improvementArea": "communication",  // 需要改进的领域。可能选项: "communication", "coding standards", "testing", "time management"
            "learningPath": "leadership training" // 建议的学习路径。可能选项: "advanced algorithms", "leadership training", "project management", "public speaking"
        }
    ],
    "skillLevel": [
        {
            "skill": "Java",
            "level": "A"  // A: 高级 (Advanced), B: 中级 (Intermediate), C: 初级 (Beginner), S: 专家 (Expert)
        },
        {
            "skill": "JavaScript",
            "level": "B"
        },
        {
            "skill": "Markdown",
            "level": "S"
        }
    ],
    "potentialStrengths": [
        {
            "area": "Microservices Architecture",  // 微服务架构
            "description": "Strong understanding and implementation skills in designing and managing microservices."  // 对设计和管理微服务有深入理解和实施技能
        },
        {
            "area": "Performance Optimization",  // 性能优化
            "description": "Expert in optimizing application performance and system resources."  // 专注于优化应用性能和系统资源
        },
        {
            "area": "DevOps Practices",  // DevOps 实践
            "description": "Proficient in continuous integration, deployment pipelines, and automated testing."  // 精通持续集成、部署管道和自动化测试
        },
        {
            "area": "Data Security",  // 数据安全
            "description": "Experience in implementing security best practices and protecting sensitive data."  // 具备实施安全最佳实践和保护敏感数据的经验
        },
        {
            "area": "API Design",  // API 设计
            "description": "Skill in designing and documenting RESTful APIs for robust integration."  // 设计和文档化 RESTful API 的技能
        },
        {
            "area": "Unit Testing",  // 单元测试
            "description": "Knowledgeable in writing and maintaining unit tests to ensure code reliability."  // 编写和维护单元测试以确保代码可靠性的知识
        },
        {
            "area": "Cloud Infrastructure",  // 云基础设施
            "description": "Familiar with setting up and managing cloud resources and services."  // 熟悉设置和管理云资源和服务
        },
        {
            "area": "Database Management",  // 数据库管理
            "description": "Experience in managing and optimizing relational and NoSQL databases."  // 管理和优化关系型及 NoSQL 数据库的经验
        }
    ]
}
```