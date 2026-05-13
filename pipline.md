def transform_data(file_path):
    df = pd.read_csv(file_path)

    # Clean columns
    df.columns = df.columns.str.strip().str.lower()

    # Clean Customer name
    df['customer_name'] = df['customer_name'].str.strip().str.title()

    # Clean products
    df['product'] = df['product'].str.replace(',', '')

    # Clean country
    df['country'] = df['country'].str.strip().str.lower()
    df['country'] = df['country'].replace(format_country_name)

    # Clean prices
    df['price'] = pd.to_numeric(df['price'], errors="coerce").fillna(0)

    # Clean quantity
    df['quantity'] = df['quantity'].str.lower()
    df['quantity'] = df['quantity'].replace(change_to_num)
    df['quantity'] = pd.to_numeric(df['quantity'], errors="coerce").fillna(0)

    # Clean Shipping date
    df['shipping_date'] = pd.to_datetime(df['shipping_date'], errors="coerce")

    # Clean Discount
    df['discount'] = pd.to_numeric(df['discount'], errors="coerce").fillna(0)

    # Remove duplicates
    cleaned_data_frame = df.drop_duplicates()

    logging.info(f"Transformation complete {PIPELINE_SUCCESS}")
    return cleaned_data_frame
