from behave import given, when, then
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.common.by import By
import time

@given('I am on the Google homepage')
def step_google_homepage(context):
    context.driver = webdriver.Chrome()  # Make sure the chromedriver is in your PATH
    context.driver.get("https://www.google.com")

@when('I search for "{search_term}"')
def step_search_term(context, search_term):
    search_box = context.driver.find_element(By.NAME, "q")
    search_box.send_keys(search_term)
    search_box.send_keys(Keys.RETURN)
    time.sleep(2)  # Wait for the search results to load

@then('I should see results related to "{search_term}"')
def step_see_results(context, search_term):
    assert search_term in context.driver.page_source
    context.driver.quit()
