# DNS Lab Exercise

## Prerequisites

- This lab uses the Domain Controller (`DC-1`) and Client VM (`Client-VM`) from the previous lab to explore DNS (Domain Name Services) setup and troubleshooting.
- If you haven’t done the previous lab, follow the initial instructions for setting up `DC-1` and `Client-VM` in the Azure cloud.

---

## A-Record Observation and Configuration Exercise

This section demonstrates how to create a basic DNS A-record and verify name resolution from a client machine.

1. Using RDP, log in to `DC-1` as an admin.
2. Using RDP, log in to `Client-VM` as an admin.
3. From `Client-VM`, open PowerShell and attempt to ping the domain name `mainframe`. Observe that the ping is unsuccessful.
4. Perform an `nslookup` for the `mainframe` domain. It should fail.
5. Now on `DC-1`, open **Administrative Tools** > **DNS**.
6. In the DNS Manager window:
   - Expand the `DC-1` folder.
   - Select **Forward Lookup Zones**.
   - Expand your domain folder, e.g., `mydomain.com`.
7. Create a DNS A-record for `mainframe` pointing to DC-1’s private IP:
   - Right-click the right-hand pane and select **New Host (A or AAAA)...**
   - Name the new host `mainframe`, and set its IP address to DC-1's private IP (use `ipconfig` to find it).
   - Check the box to create an associated pointer (PTR) record.
8. Return to `Client-VM` and ping `mainframe` again. It should now be successful.

---

## Local DNS Cache Exercise

This section demonstrates how to observe and flush the local DNS cache — useful for troubleshooting DNS issues.

1. On `DC-1`, change `mainframe`’s IP address to `8.8.8.8`:
   - Double-click the `mainframe` A-record and update the IP field.
2. On `Client-VM`, ping `mainframe` — it will still ping the old address.
3. Observe the DNS cache using:
   ```powershell
   `ipconfig /displaydns`
4. Flush the DNS cache using:
   ```powershell
   `ipconfig /displaydns`
5.Observe the changes using:
   ```powershell
   `ipconfig /displaydns`
6. Now Ping "mainframe" to observe the new address

---

## CNAME Record Exercise

Createing a CNAME record to alias a hostname and observe how it resolves from the client side.

1. In DC-1, use the DNS Manager to create a new CNAME called "search" that redirects to www.google.com
  -Follow the same steps for creating an A-Record, but this time select CNAME instead
2. From the Client-VM ping "search" in PowerShell and observe the interaction with www.google.com
3. Perform a Nslookup for "search" and observe the results

---

## This concludes the Lab

