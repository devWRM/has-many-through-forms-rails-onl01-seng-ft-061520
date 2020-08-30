
NEED Detailed explanation of this process

NOTE In a basic has many through model, the (original) single belongs_to (of the 2 has_many throughs) has the assigning attributes method
    Example

        def categories_attributes=(category_attributes)
            category_attributes.values.each do |category_attribute|
                category = Category.find_or_create_by(category_attribute)
                self.post_categories.build(category: category)
            end
        end

______________________________________________________

NOTE In file app/models/post.rb does the accepts_nested_attributes_for method replace or is in addition to the categories_attributes writer ??

ANSWER Actually, the custom categories_attributes writer is replacing the standard provided accepts_nested_attributes_for method

    class Post < ActiveRecord::Base
        has_many :post_categories
        has_many :categories, through: :post_categories
        # accepts_nested_attributes_for :categories


        def categories_attributes=(category_attributes)
            category_attributes.values.each do |category_attribute|
            category = Category.find_or_create_by(category_attribute)
            self.post_categories.build(category: category)
            end
        end

    end




