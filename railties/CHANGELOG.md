*   The new `bin/rails boot` command boots the application and exits. Supports the
    standard `-e/--environment` options.

    *Xavier Noria*

*   Generate form helpers to use `textarea*` methods instead of `text_area*` methods

    *Sean Doyle*

*   Add authentication generator to give a basic start to an authentication system using database-tracked sessions.

    Generate with...

    ```
    bin/rails generate authentication
    ```

    Generated files:

    ```
    app/models/current.rb
    app/models/user.rb
    app/models/session.rb
    app/controllers/sessions_controller.rb
    app/views/sessions/new.html.erb
    db/migrate/xxxxxxx_create_users.rb
    db/migrate/xxxxxxx_create_sessions.rb
    ```

    *DHH*


*   Add not-null type modifier to migration attributes.

    Generating with...

    ```
    bin/rails generate migration CreateUsers email_address:string!:uniq password_digest:string!
    ```

    Produces:

    ```ruby
    class CreateUsers < ActiveRecord::Migration[8.0]
      def change
        create_table :users do |t|
          t.string :email_address, null: false
          t.string :password_digest, null: false

          t.timestamps
        end
        add_index :users, :email_address, unique: true
      end
    end
    ```

    *DHH*

*   Add a `script` folder to applications, and a scripts generator.

    The new `script` folder is meant to hold one-off or general purpose scripts,
    such as data migration scripts, cleanup scripts, etc.

    A new script generator allows you to create such scripts:

    ```
    bin/rails generate script my_script
    bin/rails generate script data/backfill
    ```

    You can run the generated script using:

    ```
    bundle exec ruby script/my_script.rb
    bundle exec ruby script/data/backfill.rb
    ```

    *Jerome Dalbert*, *Haroon Ahmed*

*   Deprecate `bin/rake stats` in favor of `bin/rails stats`.

    *Juan Vásquez*

*   Add internal page `/rails/info/notes`, that displays the same information as `bin/rails notes`.

    *Deepak Mahakale*

*   Add Rubocop and GitHub Actions to plugin generator.
    This can be skipped using --skip-rubocop and --skip-ci.

    *Chris Oliver*

*   Use Kamal for deployment by default, which includes generating a Rails-specific config/deploy.yml.
    This can be skipped using --skip-kamal. See more: https://kamal-deploy.org/

    *DHH*

Please check [7-2-stable](https://github.com/rails/rails/blob/7-2-stable/railties/CHANGELOG.md) for previous changes.
