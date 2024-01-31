+++
title = 'Poem'
date = 2024-01-31T11:45:57+08:00
draft = false

+++

## 后端

1. ```
   public void delete(List<String> ids){
           DocExample docExample = new DocExample();
           docExample.setOrderByClause("sort ASC");
           DocExample.Criteria criteria = docExample.createCriteria();
           criteria.andIdIn(ids);
           docMapper.deleteByExample(docExample);
       }
   ```

## 前端

1. ```
   /**
    * 查找整根树枝
    */
   
   const ids: Array<String> = [];
   //let是一个变量，声明为const是因为这里是数组类型，为引用类型，所以这个ids是不会变化的，所以用常量即可
   const getDeleteIds = (treeSelectData: any,id: any) => {
     // console.log(treeSelectData,id)
     //遍历数组，即遍历某一层节点
     for( let i = 0;i<treeSelectData.length;i++){
       const node = treeSelectData[i];
       if (node.id === id){
         //如果当前节点就是目标节点
         console.log("disabled",node);
         //将目标id放入结果集ids中
         ids.push(id);
         //遍历所有子节点，将所有子节点全部都加上disabled
         const children = node.children;
         if (Tool.isNotEmpty(children)){
           for (let j =0;j< children.length;j++){
             getDeleteIds(children,children[j].id);
           }
         }
       }else{
         //如果当前节点不是目标节点，则到其子节点再找找看
         const children =node.children;
         if (Tool.isNotEmpty(children)){
           getDeleteIds(children,id);
         }
       }
     }
   }
   ```

2. ```
   //删除
       const handleDelete= (id: number) => {
         getDeleteIds(level1.value,id);
         axios.delete("/doc/delete/"+ids.join(",")).then((response)=>{
           const data = response.data;
           if (data.success){
             // router.go(0);
             //重新加载列表
             handleQueryDoc();
   
           }
         });
       };
   ```
