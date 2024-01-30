# Exporting Data as CSV

## Define a Class method
For example, if you wanted to export Photos records from Photogram.

In the `photo.rb` model, define a class method called `to_csv`.

```rb
class Photo < ApplicationRecord

  # ...
  def self.to_csv
    # ...
  end
end
```

### Choose the headers

You need to choose what headers you want to appear in the generated CSV. Create a variable called `headers` that contains an Array with each of the headers that you want to appear in the generated CSV.

```rb
class Photo < ApplicationRecord

  # ...
  def self.to_csv
    photos = self.all 
    headers = ["id", "caption", "image", "owner_id"]
    csv = CSV.generate(headers: true) do |csv|
      csv << headers
      # ...
    end
    return csv
  end
end
```

`self.all` is similar to `Photo.all`. `photos` determines which `Photo` records will enter the exported CSV.

### Choose the value for each row in the CSV

For the other rows besides the header, add a loop over your list of records (`photos`, in this case).

Inside the loop, create an Array that represents all the data that will appear in each row. The value and order of the elements in this `row` Array should match the order of values in the headers.

```rb
class Photo < ApplicationRecord

  # ...
  def self.to_csv
    photos = self.all
    headers = ["id", "caption", "image", "owner_id"]
    csv = CSV.generate(headers: true) do |csv|
      csv << headers
      photos.each do |photo|
        row = []
        row.push(photo.id)
        row.push(photo.caption)
        row.push(photo.image)
        row.push(photo.owner_id)
        csv << row
      end
    end
    return csv
  end
end
```

## Create a route to download the file

```rb
# config/routes.rb
get("/export_photos", { :controller => "photos", :action => "export" })

# app/controllers/photos_controller.rb
class PhotosController < ApplicationController
  # ...
  def export
    photos = Photo.all
    respond_to do |format|
      format.csv do 
        send_data(photos.to_csv, { :filename => "my_photos.csv"})
      end
    end
  end
  # ...
end
```

## Add download link to View template

```html
<a href="/export_photos.csv">Export as CSV</a>
```

Now clicking on "Export as CSV should open the download file dialog with the generated CSV.
