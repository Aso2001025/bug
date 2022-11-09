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
        name
        icon
        mail
        password
        reg_date_on
    }
    
    entity "レシピ" as recipe <recipe> <<T,TRANSACTION_MARK_COLOR>> {
        + recipe_id [PK]
        --
        # user_id [FK]
        name
        image
        explan
        point
        processed_flag
        browes
        reg_date_on
        deleted_flag
    }
    
    entity "レシピ材料" as recipe_material  <recipe_material> <<T,TRANSACTION_MARK_COLOR>> {
        + material_id[PK]
        --
        # recipe_id [FK]
        name
        amount
    }
    
    entity "レシピ詳細" as recipe_detail <recipe_detail> <<T,TRANSACTION_MARK_COLOR>> {
        + datail_id [PK]
        --
        # recipe_id [FK]
        image
        context
        deleted_flag
    }
    
     entity "タグ" as tag <tag> <<T,TRANSACTION_MARK_COLOR>> {
        + tag_id [PK]
        --
        name
        deleted_flag
    }
    
     entity "レシピタグ" as recipe_tag <recipe_tag> <<T,TRANSACTION_MARK_COLOR>> {
        + recipe_id [PK][FK]
        + tag_id [PK][FK]
        --
        deleted_flag
        
    }
    
    entity "コメント" as comment <comment> <<T,TRANSACTION_MARK_COLOR>> {
        + comment_id [PK]
        --
        user_id [FK]
        recipe_id [FK]
        context
        reg_date_on
        deleted_flag
    }
    
    entity "お気に入り" as  <favorites> <<M,MASTER_MARK_COLOR>> {
        + favorite_id [PK]
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
recipe_tag }o---||    tag
user       ||-r-o{    comment
user       ||---o|    good
recipe     ||-l-o{    comment
recipe     ||---o{    good


@enduml
```
