{{date: YYYY-MM-DD}}
Tags:# [[]]

Learn this block of code:
```python
max_retries = 3

retry_delay = 5

copied_files = {}

for i in range(3):

    retries = 0

    while retries < max_retries:

        try:

            print(f"Retry number: {retries}")

            print(f"Making a copy of MAWV Dashboard {mawv_today} - R{i + 1}")

            copy_name = f"MAWV Dashboard {mawv_today} - R{i + 1}"

            copy_name, copy_id = copy_google_drive_file(

                service_account_file=service_account_file,

                scopes=scopes,

                copy_name=copy_name,

                folder_id=template_folder_id,

                original_id=mawv_dashboard_template_ids[i]

            )

  

            copied_files[f"r{i + 1}_mawv_copy_file_name"] = copy_name

            copied_files[f"r{i + 1}_mawv_copy_file_id"] = copy_id

            # If successful, break the retry loop

            break

        except Exception as e:

            retries += 1

            print(f"Attempt {retries} failed for file MAWV Dashboard {mawv_today} - R{i + 1}: {e}")

            # If this was the last retry, raise the exception

            if retries == max_retries:

                print(f"Failed to copy file after {max_retries} attempts.")

                raise

            # Wait before retrying

            time.sleep(retry_delay)
```



---
### Reference