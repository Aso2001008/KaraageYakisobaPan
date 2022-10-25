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

package "Gohunt" as target_system {
    
    
    entity "ユーザーマスタ" as users  <m_users> <<M,MASTER_MARK_COLOR>> {
        + user_id[PK]
        --
        user_name
        user_mail
        user_pass
        age
        sex_Flag
        reg_date
        upd_date
    }
    
    entity "ショップマスタ" as shop  <m_shop> <<M,MASTER_MARK_COLOR>> {
        +shop_id[PK]
        --
        shop_name
        shop_name_rubi
        # user_id [FK]
        reg_date
        upd_date
    }
    
    entity "ショップアドレスマスタid" as shopAddress_id  <m_shopAddress_id> <<M,MASTER_MARK_COLOR>> {
        +shop_id[PK]
        --
        #shop_address_id[FK]
    }
    
    entity "ショップアドレスマスタ" as shopAddress  <m_shopAddress> <<M,MASTER_MARK_COLOR>> {
        +shop_address_id[PK]
        --
        shop_latitude
        shop_longitude
        shop_address
        reg_date
        upd_date
    }
    
    entity "タグidマスタ" as tag_id  <m_tag_id> <<M,MASTER_MARK_COLOR>> {
        +shop_id[PK]
        --
        #tag_id[FK]
    }
    
    entity "タグマスタ" as tag  <m_tag> <<M,MASTER_MARK_COLOR>> {
        +tag_id[PK]
        --
        tag_name
        reg_date
        upd_date
    }
    
    entity "ショップ説明テーブルid" as shopExplanation_id <m_shopExplanation_id> <<T,TRANSACTION_MARK_COLOR>> {
        +shop_explanation_id [PK]
        --
        #shop_id[FK]
    }
    
    entity "ショップ説明テーブル" as shopExplanation <t_shopExplanation> <<T,TRANSACTION_MARK_COLOR>> {
        +shop_explanation_id [PK]
        --
        #shop_id[FK]
        shop_explanation
        # shop_address_id [FK]
        # shop_image_id [FK]
        # tag_id [FK]
        # user_id [FK]
        reg_date
        upd_date
    }
    
    entity "ショップ画面マスタid" as shopImage_id <m_shopImage_id> <<M,MASTER_MARK_COLOR>> {
        +shop_image_id [PK]
        --
        #shop_id[FK]
    }
    
    entity "ショップ画面マスタ" as shopImage <m_shopImage> <<M,MASTER_MARK_COLOR>> {
        +shop_image_id [PK]
        --
        shop_image
        # user_id [FK]
        reg_date
        upd_date
    }
    
    entity "ショップ評価マスタid" as shopEvaluation_id <m_shopEvaluation_id> <<M,MASTER_MARK_COLOR>> {
        +shop_id[PK]
        --
        #shop_evaluation_id[FK]
    }
    
    entity "ショップ評価マスタ" as shopEvaluation <m_shopEvaluation> <<M,MASTER_MARK_COLOR>> {
        +shop_evaluation_id[PK]
        --
        shop_Appearance_evaluation
        shop_atmosphere_evaluation
        shop_taste_evaluation
        reg_date
        upd_date
    }
    
   }
  
  users     }--{      shopExplanation
  shopImage_id     }--{      shopExplanation
  tag_id     }--{      shopExplanation
  tag     }--{      tag_id
  shopImage     }--{      users
  shop     }--{      users
  shopExplanation     }--{      shopAddress_id
  shopAddress     }--{      shopAddress_id
  shop     }--{      shopImage_id
  shopImage     }--{      shopImage_id
  shop     }--{      shopAddress
  shopEvaluation_id    }--{    shopExplanation
  shopEvaluation_id    }--{    shopEvaluation
  shopEvaluation    }--{    users
  
  
@enduml
```
