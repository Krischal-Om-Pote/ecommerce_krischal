OBJECTIVES:

1. To implement the search operations in the modeles.
2. Implement the image tag to store and display image in the product model.

INTRODUCTION:
In application search works like a regular search engine. Users type in their query, and then can view their search result.

PROCEDURE:

1.  In 'admin.py' implement the following code:

    class ProductAdmin(admin.ModelAdmin):
    list_display = ["name", "price", "brand", "category",]
    search_fields = ["name", "price", "brand__name", "category__name",]
    list_filter = ["brand","category",]
    readonly_fields = ["quantity",]
    class Meta:
    model = Product
    admin.site.register(Product, ProductAdmin)

    in this code the **"search_fiels"** is the field implemeted for the usage of search for the refrenced table i.e the brand table whose **primary key** is refrenced as a **foreign key**.

2.  Similarly implement the same changes in other models as well:

        #Implementaion of search in the brand model:
        class BrandAdmin(admin.ModelAdmin):
            list_display = ["name",]
            search_fields = ["name",]
            class Meta:
                model = Brand
        admin.site.register(Brand, BrandAdmin)

        #Implementation of search in the category model:
        class CategoryAdmin(admin.ModelAdmin):
            list_display = ["name",]
            search_fields = ["name",]
            class Meta:
                model = Category
        admin.site.register(Category, CategoryAdmin)

3.  Add the field for displaying the image in the list view. For this add a field **"image_tag"** to the product class in the 'models.py' to enter the image urls in the database.

            #import the mark_safe from the django.utils.html first:
            from django.utils.html import mark_safe

            # add the following code to add the image_url field in the model:
            class Product(models.Model):
            ...
                def image_tag(self):
                    return mark_safe(f'<img src="{self.image_url}" width="50" height="50" />')
                image_tag.short_description = "Product"
                def __str__(self):
                    return self.name

    the usage of mark_safe is to mark a custom string as a safe string for
    HTML/output rendering.

4.  In the class **ProductAdmin** in 'admin.py' implement the follwing changes:

        class ProductAdmin(admin.ModelAdmin):
            list_display = ["image_tag", "name", "price", "brand", "category",]
            search_fields = ["name", "price", "brand__name", "category__name",]
            list_filter = ["brand","category","price",]
            # readonly_fields = ["quantity",]
            class Meta:
            model = Product
        admin.site.register(Product, ProductAdmin)

5.  Run the project and navigate to admin to check the reesult

        python manage.py runserver

OUTPUTS:
![image of search in Brands module](https://github.com/Krischal-Om-Pote/ecommerce_krischal/blob/master/ecommerce_krischal/output/lab3/1.png);

![image of search in Category module](https://github.com/Krischal-Om-Pote/ecommerce_krischal/blob/master/ecommerce_krischal/output/lab3/2.png);

![image of search in Products module](https://github.com/Krischal-Om-Pote/ecommerce_krischal/blob/master/ecommerce_krischal/output/lab3/3.png);

CONCUSION:
Hence,i have learn how to implement the search engine in a particular module, insert the images in the database by entering the images link address and displaying it in the list view.
