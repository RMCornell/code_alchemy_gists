# ===== Controllers =====

## Controller Basics
Controller files are held in the controllers directory under the app folder (app_root/app/controllers)
Each model will need an associated controller
Controller names are plural of the model they are controlling

If you use rails generate scaffold, rails will create and populate a basic controller set upu with details on what the controller does and attached routes.

The controller holds the actions that are associated with different routes that will be visited by users during interaction with the app.  

Basic Controller operations are related to the routes defined in app_root/config/routes.rb


    Controller Method   HTTP Verb             URL                                 prefix(always add _path to end)
        -#index             GET                /<model_name>(plural)               users_path
                                              -/users
                                              
        -#create            POST               /<model_name>(plural)               users_path method: :post
                                              -/users
                                              
        -#new               GET                /<model_name>(plural)/new           new_user_path
                                              -/users/new
                                              
        -#edit              GET                /<model_name>(plural)/:id/edit      edit_user_path
                                              -/users/1/edit (edits user id 1 where 1 is params([:id])
        
        -#show              GET                /<model_name>(plural)/:id           user_path(params[:id])?    
                                              -/users/1 (shows user 1 where 1 is (params[:id])
                                              
        -#update            PATCH              /model_name>(plural)/:id            user_path(params[:id]) method: :patch?
                                              -/users/1
        
        -#update            PUT                /<model_name>(plural)/:id           user_path(params[:id]) method: :put?
                                              -/users/1
        
        -#destroy           DELETE             /<model_name>(plural)/:id           user_path(params[:id]) method: :destroy?
                                              -/users/1
                                              
## Writing Controller Actions - Index
Index is the point that will display all of a given models objects.  Depending on what is wanted to be shown, this is typically a listing of all users, all pets, or all x of a given model

    In app_root/app/controllers/model_controller: 
    def index
        @model_name(plural) = modelname(singular).all
    end
    
    Example:
    def index
        @users = User.all
    end
    
This will provide a full hash of users from within the database from the Users table. 

        #<ActiveRecord::Relation [#<User id: 1, username: "legend", password_digest: "$2a$10$X8/Nf/nFeAxt1oOA86EuEe24vuDwn.2OPKw8b8z8mlT...", first_name: "John", last_name: "Legend", created_at: "2015-06-12 05:12:21", updated_at: "2015-06-12 05:12:21">, 
        #<User id: 2, username: "usher", password_digest: "$2a$10$4sCvSfavznqLK19PK0bA../4YsB62a/.lNcR5Pqkvyi...", first_name: "Usher", last_name: "Usher", created_at: "2015-06-12 05:15:33", updated_at: "2015-06-12 05:15:33">]>
        
        -looking through the hash you can see specific columns of the users table and their values: 
            -User_id: (generated and auto incremented by active record)
            -username: (generated at creation of user - usually from user input
            -password_digest: (generated at creation of user - usually from user input but displayed in db as encrypted password using bcrypt
            -first_name: (generated at creation of user - usually from user input)
            -last_name: (generated at creation of user - usually from user input)
            -created_at (generated by active record)
            -updated_at (generated by active record)
                