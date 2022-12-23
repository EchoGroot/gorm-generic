# gorm-generic

+ Gorm的辅助工具类，提供了基础的CRUD方法，通过泛型实现。
+ 命名参照[mybatisplus的mapper](https://baomidou.com/pages/49cc81/#mapper-crud-%E6%8E%A5%E5%8F%A3)
+ **注意：error已经使用过errors.Wrap()了，切勿重复wrap！**

## 安装

```bash
go get github.com/echogroot/gorm-generic
```

## 使用

### 初始化repo

```go
package main

import (
	"time"

	"github.com/echogroot/gorm-generic/repo"
	"gorm.io/gorm"
)

type User struct {
	Id         string    `gorm:"primaryKey,type:uuid"`
	CreateTime time.Time `gorm:"autoCreateTime"`
}

func (User) TableName() string {
	return "user"
}

type UserRepo struct {
	repo.BaseRepo[User]
}

func NewUserRepo(db *gorm.DB) *UserRepo {
	return &UserRepo{
		BaseRepo: repo.NewBaseRepo[User](db),
	}
}

```
