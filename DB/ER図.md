```uml
@startuml
skinparam class {
    '図の背景
    BackgroundColor Snow
    '図の枠
    BorderColor Black
    'リレーションの色
    ArrowColor Black
}
!define MASTER_MARK_COLOR Orange 
!define TRANSACTION_MARK_COLOR DeepSkyBlue
package "ECサイト" as target_system {
    /'
      マスターテーブルを M、トランザクションを T などで表記
      １文字なら "主" とか "従" まど日本語でも記載可能
     '/
    entity "ユーザー" as user <user> <<M,MASTER_MARK_COLOR>> {
        + user_id [PK]
        --
        user_name
        icon
        mail
        password
        lebel
        birthday
        reg_date
    }
    
    entity "レシピ" as recipe <recipe> <<T,TRANSACTION_MARK_COLOR>> {
        + recipe_id [PK]
        --
        # user_id [FK]
        recipe_naem
        recipe_image
        explan
        point
        # category_id [FK]
        time
        processed_flag
        good
        browes
        keep
        reg_date
    }
    
    entity "レシピ材料" as recipe_material  <recipe_material> <<T,TRANSACTION_MARK_COLOR>> {
        + material_id[PK]
        --
        # recipe_id [FK]
        material_name
        amount
    }
    
    entity "レシピ詳細" as recipe_detail <recipe_detail> <<T,TRANSACTION_MARK_COLOR>> {
        + datail_id [PK]
        --
        # recipe_id [FK]
        procedure
        detail_image
        detail_text
    }
    
     entity "タグ" as tag <tag> <<T,TRANSACTION_MARK_COLOR>> {
        + tag_id [PK]
        --
        tag_name
        
    }
    
     entity "レシピタグ" as recipe_tag <recipe_tag> <<T,TRANSACTION_MARK_COLOR>> {
        + recipe_id [PK][FK]
        + tag_id [PK][FK]
        --
        
    }
    
    entity "コメント" as comment <comment> <<T,TRANSACTION_MARK_COLOR>> {
        + comment_id [PK]
        --
        user_id [FK]
        recipe_id [FK]
        text
        reg_date
    }
    
    entity "いいね" as good <good> <<M,MASTER_MARK_COLOR>> {
        + good_id [PK]
        --
        user_id [FK]
        recipe_id [FK]
        reg_date
    }
    
    entity "保存" as keep <keep> <<M,MASTER_MARK_COLOR>> {
        + keep_id [PK]
        --
        user_id [FK]
        recipe_id [FK]
        reg_date
    }
    
  }
  
user       ||-r-o{    recipe
recipe     ||-r-|{    recipe_detail
recipe     ||-u-|{    recipe_material
recipe     }o---||    recipe_tag

user       ||-r-o{    comment
user       ||---o{    keep
user       ||---o|    good
recipe     ||-l-o{    comment
recipe     ||---o{    keep
recipe     ||---o{    good

@enduml
```
