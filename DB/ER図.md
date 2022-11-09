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
    entity "ユーザー" as users <users> <<M,MASTER_MARK_COLOR>> {
        + user_id [PK]
        --
        name
        icon
        mail
        password
        reg_date_on
    }
    
    entity "レシピ" as recipes <recipes> <<T,TRANSACTION_MARK_COLOR>> {
        + recipe_id [PK]
        --
        # user_id [FK]
        name
        image
        explan
        point
        image_blurred
        browes
        reg_date_on
        deleted_flag
    }
    
    entity "レシピ材料" as recipe_materials  <recipe_materials> <<T,TRANSACTION_MARK_COLOR>> {
        + material_id[PK]
        --
        # recipe_id [FK]
        name
        amount
    }
    
    entity "レシピ手順" as recipe_procedures <recipe_procedures> <<T,TRANSACTION_MARK_COLOR>> {
        + procedure_id [PK]
        --
        # recipe_id [FK]
        image
        context
        deleted_flag
    }
    
     entity "タグ" as tags <tags> <<T,TRANSACTION_MARK_COLOR>> {
        + tag_id [PK]
        --
        name
        deleted_flag
    }
    
     entity "レシピタグ" as recipe_tags <recipe_tags> <<T,TRANSACTION_MARK_COLOR>> {
        + recipe_id [PK][FK]
        + tag_id [PK][FK]
        --
        deleted_flag
        
    }
    
    entity "コメント" as comments <comments> <<T,TRANSACTION_MARK_COLOR>> {
        + comment_id [PK]
        --
        user_id [FK]
        recipe_id [FK]
        context
        reg_date_on
        deleted_flag
    }
    
    entity "お気に入り" as favorites <favorites> <<M,MASTER_MARK_COLOR>> {
        + favorite_id [PK]
        --
        user_id [FK]
        recipe_id [FK]
        reg_date
    }
    
    
    
  }
  
users       ||-r-o{    recipes
recipes     ||-r-|{    recipe_procedures
recipes     ||-u-|{    recipe_materials
recipes     }o---||    recipe_tags
recipe_tags }o---||    tags
users       ||-r-o{    comments
users       ||---o|    favorites
recipes     ||-l-o{    comments
recipes     ||---o{    favorites


@enduml
```
