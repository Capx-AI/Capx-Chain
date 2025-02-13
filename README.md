# Capx Chain 

Network details for the Capx blockchain, currently in testnet. The data is stored in JSON format, making it easy to use in applications and scripts.

## Testnet Details

| **Property**                    | **Details**                                                                  |
| ------------------------------- | ---------------------------------------------------------------------------- |
| **Network Name**                | Capx Testnet                                                                 |
| **Chain ID**                    | 10245                                                                        |
| **RPC URL**                     | [https://capx-testnet.alt.technology](https://capx-testnet.alt.technology)   |
| **WSS URL**                     | [wss://capx-testnet.alt.technology/ws](wss://capx-testnet.alt.technology/ws) |
| **Explorer URL**                | [https://capxscan.com](https://capxscan.com)                                 |
| **Currency Name**               | GAS                                                                          |
| **Currency Symbol**             | GAS                                                                          |
| **Currency Decimals**           | 18                                                                           |
| **Block Explorer API Base URL** | [https://capxscan.com/api](https://capxscan.com/api)                         |


The network details are stored in the `testnet.json` file. The structure of the JSON file is as follows:

```json
{
  "name": "Network Name",
  "chain_id": Chain ID (number),
  "rpc_url": "RPC Endpoint URL",
  "wss_url": "WebSocket Endpoint URL (if available)",
  "explorer": "Block Explorer URL",
  "currency": {
    "name": "Currency Name",
    "symbol": "Currency Symbol",
    "decimals": Number of decimal places
  },
  "block_explorer_api": {
    "base_url": "Base URL for API calls"
  }
}
```

## How to Use

1. **Clone the repository:**

    ```bash
    git clone https://github.com/Capx-AI/Capx-Chain.git
    ```

2. **Access network details:**

    You can use any programming language or tool that can read JSON files to access the network details. 
    
    For example, in Python:

    ```python
    import json

    with open('testnet.json', 'r') as f:
        network_data = json.load(f)

    print(network_data['name'])      # Output: Capx Testnet
    print(network_data['rpc_url'])   # Output: https://capx-testnet.alt.technology
    ```

## Capxscan API 

**Base URL:** `https://capxscan.com/api`

**Documentation:** [https://capxscan.com/api-docs](https://capxscan.com/api-docs)

## Capxscan RESTful API Endpoints

In addition to the standard `module=...&action=...` API format, Capxscan also provides RESTful API endpoints for retrieving more detailed information. These endpoints do not require an API key.

Here are some useful Capxscan RESTful API endpoints with Python examples:

**1. Get Address Info**

*   **Endpoint:** `/addresses/{address_hash}`
*   **Method:** `GET`
*   **Description:** Retrieves information about a specific address, including balance, transaction count, and code (if it's a contract).
*   **Example:** `/addresses/0xBC7a2925D5C194D1DbEdeB99F13c326851dC8230`

```python
import requests

def get_address_info(address_hash):
  """Retrieves information about an address.

  Args:
    address_hash: The address hash (e.g., "0x...").

  Returns:
    A dictionary containing address information, or None if an error occurred.
  """
  url = f"https://capxscan.com/addresses/{address_hash}"
  try:
    response = requests.get(url)
    response.raise_for_status()
    return response.json()
  except requests.exceptions.RequestException as e:
    print(f"Error: {e}")
    return None

# Example usage:
address_hash = "0xBC7a2925D5C194D1DbEdeB99F13c326851dC8230"  # Replace with a real address hash
address_info = get_address_info(address_hash)
if address_info:
  print(f"Address Info for {address_hash}:")
  print(f"  - Balance: {int(address_info['coin_balance']) / (10**18)} GAS")
  print(f"  - Contract: {address_info['is_contract']}")
```

**2. Get Address Logs**

*   **Endpoint:** `/addresses/{address_hash}/logs`
*   **Method:** `GET`
*   **Description:** Retrieves event logs associated with a specific address.
*   **Example:** `/addresses/0xBC7a2925D5C194D1DbEdeB99F13c326851dC8230/logs`

```python
import requests

def get_address_logs(address_hash):
  """Retrieves event logs for an address.

  Args:
    address_hash: The address hash (e.g., "0x...").

  Returns:
    A list of event logs, or None if an error occurred.
  """
  url = f"https://capxscan.com/addresses/{address_hash}/logs"
  try:
    response = requests.get(url)
    response.raise_for_status()
    return response.json()
  except requests.exceptions.RequestException as e:
    print(f"Error: {e}")
    return None
```

**3. Get All Token Balances for an Address**

*   **Endpoint:** `/addresses/{address_hash}/token-balances`
*   **Method:** `GET`
*   **Description:** Retrieves all token balances (ERC20, ERC721, etc.) for a specific address.
*   **Example:** `/addresses/0xBC7a2925D5C194D1DbEdeB99F13c326851dC8230/token-balances`

```python
import requests

def get_address_token_balances(address_hash):
  """Retrieves all token balances for an address.

  Args:
    address_hash: The address hash (e.g., "0x...").

  Returns:
    A list of token balances, or None if an error occurred.
  """
  url = f"https://capxscan.com/addresses/{address_hash}/token-balances"
  try:
    response = requests.get(url)
    response.raise_for_status()
    return response.json()
  except requests.exceptions.RequestException as e:
    print(f"Error: {e}")
    return None
```

**4. Get Block Info**

*   **Endpoint:** `/blocks/{block_number_or_hash}`
*   **Method:** `GET`
*   **Description:** Retrieves information about a specific block, identified by its number or hash.
*   **Example:** `/blocks/1000` or `/blocks/0x555d5fcb344d21e0a956a97677d7477d47d454da589c945544bf8b55d944d6aa`

```python
import requests

def get_block_info(block_identifier):
  """Retrieves information about a block.

  Args:
    block_identifier: The block number (as an integer) or block hash (as a string).

  Returns:
    A dictionary containing block information, or None if an error occurred.
  """
  url = f"https://capxscan.com/blocks/{block_identifier}"
  try:
    response = requests.get(url)
    response.raise_for_status()
    return response.json()
  except requests.exceptions.RequestException as e:
    print(f"Error: {e}")
    return None
```

**5. Get Transaction Info**

*   **Endpoint:** `/transactions/{transaction_hash}`
*   **Method:** `GET`
*   **Description:** Retrieves information about a specific transaction.
*   **Example:** `/transactions/0x91160418f64e2937927deca07063f408aa08b18a5955f39f49cfe2f301d8fd0d`

```python
import requests

def get_transaction_info(transaction_hash):
  """Retrieves information about a transaction.

  Args:
    transaction_hash: The transaction hash (e.g., "0x...").

  Returns:
    A dictionary containing transaction information, or None if an error occurred.
  """
  url = f"https://capxscan.com/transactions/{transaction_hash}"
  try:
    response = requests.get(url)
    response.raise_for_status()
    return response.json()
  except requests.exceptions.RequestException as e:
    print(f"Error: {e}")
    return None
```

**6. Get Token Info**

*   **Endpoint:** `/tokens/{token_address}`
*   **Method:** `GET`
*   **Description:** Retrieves information about a specific token (ERC20, ERC721, etc.).
*   **Example:** `/tokens/0xBC7a2925D5C194D1DbEdeB99F13c326851dC8230`

```python
import requests

def get_token_info(token_address):
    """Retrieves information about a token.

    Args:
      token_address: The token contract address (e.g., "0x...").

    Returns:
      A dictionary containing token information, or None if an error occurred.
    """
    url = f"https://capxscan.com/tokens/{token_address}"
    try:
        response = requests.get(url)
        response.raise_for_status()
        return response.json()
    except requests.exceptions.RequestException as e:
        print(f"Error: {e}")
        return None
```

**7. Get Token Transfers**

*   **Endpoint:** `/tokens/{token_address}/transfers`
*   **Method:** `GET`
*   **Description:** Retrieves a list of transfers for a specific token.
*   **Example:** `/tokens/0xBC7a2925D5C194D1DbEdeB99F13c326851dC8230/transfers`

```python
import requests

def get_token_transfers(token_address):
    """Retrieves a list of transfers for a token.

    Args:
        token_address: The token contract address (e.g., "0x...").

    Returns:
        A list of token transfers, or None if an error occurred.
    """
    url = f"https://capxscan.com/tokens/{token_address}/transfers"
    try:
        response = requests.get(url)
        response.raise_for_status()
        return response.json()
    except requests.exceptions.RequestException as e:
        print(f"Error: {e}")
        return None
```

**8. Get Token Holders**

*   **Endpoint:** `/tokens/{token_address}/holders`
*   **Method:** `GET`
*   **Description:** Retrieves a list of holders for a specific token.
*   **Example:** `/tokens/0xBC7a2925D5C194D1DbEdeB99F13c326851dC8230/holders`

```python
import requests

def get_token_holders(token_address):
    """Retrieves a list of holders for a token.

    Args:
        token_address: The token contract address (e.g., "0x...").

    Returns:
        A list of token holders, or None if an error occurred.
    """
    url = f"https://capxscan.com/tokens/{token_address}/holders"
    try:
        response = requests.get(url)
        response.raise_for_status()
        return response.json()
    except requests.exceptions.RequestException as e:
        print(f"Error: {e}")
        return None
```

**9. Get Contracts**

*   **Endpoint:** `/smart-contracts`
*   **Method:** `GET`
*   **Description:** Retrieves a list of verified contracts.
*   **Example:** `/smart-contracts`

```python
import requests

def get_contracts():
    """Retrieves a list of verified contracts.

    Returns:
        A list of verified contracts, or None if an error occurred.
    """
    url = "https://capxscan.com/smart-contracts"
    try:
        response = requests.get(url)
        response.raise_for_status()
        return response.json()
    except requests.exceptions.RequestException as e:
        print(f"Error: {e}")
        return None
```

**10. Search**

*   **Endpoint:** `/search`
*   **Method:** `GET`
*   **Description:** Searches for blocks, transactions, addresses, and tokens.
*   **Example:** `/search?q=0xBC7a2925D5C194D1DbEdeB99F13c326851dC8230`

```python
import requests

def search(value):
    """Searches for blocks, transactions, addresses, and tokens.

    Args:
        q: The search query (e.g., an address, transaction hash, block number, or token name).

    Returns:
        A dictionary containing search results, or None if an error occurred.
    """
    url = f"https://capxscan.com/search?q={value}"
    try:
        response = requests.get(url)
        response.raise_for_status()
        return response.json()
    except requests.exceptions.RequestException as e:
        print(f"Error: {e}")
        return None

# Example usage:
search_query = "0xBC7a2925D5C194D1DbEdeB99F13c326851dC8230"
search_results = search(search_query)
```

These RESTful API endpoints provide more flexibility and control over the data you retrieve from Capxscan. Remember to replace the example addresses, hashes, and block numbers with real values when using these in your applications.
